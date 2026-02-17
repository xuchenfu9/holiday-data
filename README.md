# Holiday Data

全球节假日数据仓库，为 SmartAlarm 应用提供节假日数据支持。

## 数据结构

```
holidays/
├── CN/          # 中国大陆
├── US/          # 美国
├── UK/          # 英国
├── JP/          # 日本
├── KR/          # 韩国
├── TW/          # 台湾
└── HK/          # 香港
```

## 数据格式

每个 JSON 文件包含一年的节假日数据：

```json
{
  "region": "CN",
  "year": 2025,
  "lastUpdated": "2025-01-15",
  "holidays": [
    {
      "date": "2025-01-01",
      "name": "元旦",
      "isOffDay": true
    }
  ]
}
```

### 字段说明

| 字段 | 类型 | 说明 |
|------|------|------|
| date | string | 日期，格式 yyyy-MM-dd |
| name | string | 节日名称 |
| isOffDay | boolean | true=放假，false=调休上班 |

## 使用方式

Raw URL 格式：
```
https://raw.githubusercontent.com/{owner}/holiday-data/main/holidays/{region}/{year}.json
```

示例：
```
https://raw.githubusercontent.com/{owner}/holiday-data/main/holidays/CN/2025.json
```

## 贡献

欢迎提交 PR 更新或修正节假日数据。

## License

MIT
