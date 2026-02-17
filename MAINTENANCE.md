# 节假日数据维护指南

## 数据获取逻辑

App 启动时会自动获取**当前年**和**下一年**的节假日数据。

### 数据源优先级

| 地区 | 优先数据源 | 备用数据源 |
|------|-----------|-----------|
| 中国大陆 | timor.tech API | GitHub |
| 美国、英国、日本、韩国 | Nager.Date API | GitHub |
| 台湾、香港 | GitHub | - |

当优先数据源请求失败时，自动回退到 GitHub 数据。

## 文件结构

```
holidays/
├── CN/          # 中国大陆
│   ├── 2025.json
│   ├── 2026.json
│   └── 2027.json
├── US/          # 美国
├── UK/          # 英国
├── JP/          # 日本
├── KR/          # 韩国
├── TW/          # 台湾
└── HK/          # 香港
```

## JSON 格式

```json
{
  "region": "CN",
  "year": 2027,
  "lastUpdated": "2026-12-01",
  "holidays": [
    {
      "date": "2027-01-01",
      "name": "元旦",
      "isOffDay": true
    }
  ]
}
```

### 字段说明

| 字段 | 类型 | 说明 |
|------|------|------|
| `region` | string | 地区代码：CN/US/UK/JP/KR/TW/HK |
| `year` | number | 年份 |
| `lastUpdated` | string | 最后更新日期 yyyy-MM-dd |
| `holidays` | array | 节假日列表 |
| `holidays[].date` | string | 日期 yyyy-MM-dd |
| `holidays[].name` | string | 节日名称 |
| `holidays[].isOffDay` | boolean | true=放假，false=调休上班 |

## 更新数据

### 方式一：GitHub 网页编辑

1. 打开 https://github.com/xuchenfu9/holiday-data
2. 进入对应目录，如 `holidays/CN/`
3. 点击要编辑的文件，或点 "Add file" 新建
4. 编辑内容后点 "Commit changes"

### 方式二：本地推送

```bash
cd /path/to/holiday-data
# 编辑文件后...
git add .
git commit -m "更新 2027 年节假日数据"
git push
```

## 新增年份

每年年底需要新增下一年的数据文件：

1. 在各地区目录下创建 `{year}.json`
2. 按照 JSON 格式填入数据
3. 提交到 GitHub

## 注意事项

- GitHub Raw URL 有 CDN 缓存，更新后可能需要几分钟生效
- 中国地区的调休日（周末上班）需要设置 `isOffDay: false`
- App 会自动获取当前年和下一年数据，无需修改代码
