# API Spec Template

## Purpose
- Laravel と frontend/mobile 間で API 契約の正本として使う。
- 型の齟齬を減らし、AI が参照しやすい形式で記述する。

## Basic Information
- API Name:
- Summary:
- Related Screen Or Feature:
- Owner Layer:

## Endpoint
- Method:
- Path:
- Authentication Required:
- Authorization Rule:

## Request
### Path Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
|      |      |          |             |

### Query Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
|      |      |          |             |

### Request Body
| Name | Type | Required | Description | Example |
|------|------|----------|-------------|---------|
|      |      |          |             |         |

### Validation Rules
- 

## Response
### Success Response
- HTTP Status:

| Name | Type | Description | Example |
|------|------|-------------|---------|
|      |      |             |         |

### Error Response
| HTTP Status | Condition | Response Shape |
|-------------|-----------|----------------|
|             |           |                |

## Business Rules
- 

## Side Effects
- DB 更新:
- External Service Call:
- Event Or Notification:

## Consistency Notes
- frontend/src/api への影響:
- frontend/src/types への影響:
- mobile/lib/services への影響:
- mobile/lib/models への影響:

## Test Viewpoints
- 正常系:
- 異常系:
- 境界値:
- 権限:
- 再実行:
