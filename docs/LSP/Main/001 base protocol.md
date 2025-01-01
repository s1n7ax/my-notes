# Base protocol

- Request consist of **header part** & a **content part**
- Header part contains **header fields**
- Header field has following syntax `key: header\r\n`
  - Key and the values is separated by `: `
  - Each field is terminated by `\r\n`
- Header itself is terminated by `\r\n`
- Supported header fields are
  - Content-Length
  - Content-Type
- Content part contains the message
- Content part is using JSON-RPC to describe the request, response & notification

```
┌────────────────────────────────────────┐
│                Request                 │
│                                        │
│                                        │
│                                        │
│ ┌────────────────────────────────────┐ │
│ │            Header part             │ │
│ │                                    │ │
│ │ Key: Value \r\n                    │ │
│ │                                    │ │
│ │                                    │ │
│ │                                    │ │
│ └────────────────────────────────────┘ │
│                                        │
│  \r\n                                  │
│                                        │
│ ┌────────────────────────────────────┐ │
│ │            Content part            │ │
│ │ {                                  │ │
│ │  "name": value                     │ │
│ │ }                                  │ │
│ │                                    │ │
│ │                                    │ │
│ └────────────────────────────────────┘ │
│                                        │
└────────────────────────────────────────┘
```

Example:-

```
Content-Length: ...\r\n
\r\n
{
	"jsonrpc": "2.0",
	"id": 1,
	"method": "textDocument/completion",
	"params": {
		...
	}
}
```
