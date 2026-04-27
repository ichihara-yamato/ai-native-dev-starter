# Laravel Frontend Asset Rules

## Purpose
- Laravel の画面実装では Vite を標準の asset bundler として扱う。
- CSS と JavaScript は共通資産とページ固有資産を分離し、不要な asset を全ページへ配布しない。

## Base Policy
- Laravel の frontend asset は Vite を前提に構成する。
- 共通で使う CSS と JavaScript は `resources/css/app.css` と `resources/js/app.js` などの共通 entry に集約する。
- ページ固有の CSS と JavaScript は、共通 entry に無秩序に追加しない。
- 1つのページだけで使う asset は、そのページにだけ読み込まれるように構成する。

## Blade Loading Policy
- Blade レイアウトでは、共通 asset は `@vite(...)` で読み込む。
- ページ固有の CSS と JavaScript は `@stack` と `@push` の組み合わせで追加する。
- ページ固有 asset を読み込むための受け口は、共通レイアウトに `@stack('styles')` と `@stack('scripts')` を配置する。
- 個別 Blade では必要な場合だけ `@push('styles')` と `@push('scripts')` を使う。

## Separation Rules
- 共通レイアウト、共通コンポーネント、複数画面で再利用する処理だけを共通 asset に置く。
- 単一画面、単一機能、単一モーダル専用の処理はページ固有 asset に分離する。
- ページ固有 asset を共通 asset に寄せるのは、再利用性が明確に確認できた場合だけにする。
- 画面ごとの都合で app.css や app.js を肥大化させない。

## Vite Entry Guidance
- Vite の entry は無制限に増やさず、共通 entry と必要最小限のページ固有 entry に抑える。
- ページ固有 entry を追加する場合は、どの画面から読み込まれるかを明確にする。
- entry 追加時は Blade 側の読み込み箇所とセットで管理する。

## Blade Example Policy
- 共通レイアウト例:
  - `@vite(['resources/css/app.css', 'resources/js/app.js'])`
  - `@stack('styles')`
  - `@stack('scripts')`
- 個別ページ例:
  - `@push('styles')` でページ専用 CSS を追加する。
  - `@push('scripts')` でページ専用 JS を追加する。

## Blade Layout Example
```blade
<head>
  @vite(['resources/css/app.css', 'resources/js/app.js'])
  @stack('styles')
</head>
<body>
  @yield('content')
  @stack('scripts')
</body>
```

## Page Asset Example
```blade
@extends('layouts.app')

@push('styles')
  @vite('resources/css/pages/users/show.css')
@endpush

@push('scripts')
  @vite('resources/js/pages/users/show.js')
@endpush

@section('content')
  <div class="user-detail-page">
    <!-- page content -->
  </div>
@endsection
```

## Prohibited Patterns
- 単一ページ専用の処理を `resources/js/app.js` に直接追記しない。
- 単一ページ専用のスタイルを `resources/css/app.css` に直接追記しない。
- Blade ごとにインライン `<script>` や巨大な `<style>` を増やして運用しない。
- `@stack` の受け口が無いレイアウトに対して `@push` だけを追加しない。

## Review Points
- このページに不要な CSS や JS が共通 asset に混ざっていないか確認する。
- 共通化した asset が本当に複数画面で再利用されているか確認する。
- Blade レイアウトと各ページの `@stack` `@push` の対応が崩れていないか確認する。