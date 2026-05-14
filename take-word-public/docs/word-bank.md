# 词库格式

Take Word 支持导入 CSV 词库。建议使用 UTF-8 编码保存文件。

## 推荐表头

```csv
word,meaning,phonetic,example,tags,audio
```

建议保留表头。如果第一列为 `word`，第二列为 `meaning` 或 `definition`，应用会自动把第一行作为表头处理。

## 字段说明

| 字段 | 是否必填 | 说明 |
| --- | --- | --- |
| `word` | 必填 | 要练习的英文单词、短语或字母。 |
| `meaning` | 必填 | 中文释义或简短解释。 |
| `phonetic` | 可选 | 音标。 |
| `example` | 可选 | 例句。 |
| `tags` | 可选 | 标签，可用英文分号 `;` 或竖线 `|` 分隔。 |
| `audio` | 可选 | 发音音频的本地路径或 URI。 |

## 示例

```csv
word,meaning,phonetic,example,tags,audio
apple,苹果,/ˈæpəl/,I ate an apple.,noun;food,
book,书,/bʊk/,Read a book.,noun,
oral,"n. 口试\na. 口头的，口述的，口部的",/ˈɔːrəl/,The oral exam starts today.,exam,
```

`meaning` 中可以写入 `\n`。应用显示时会转换为真实换行。

## CSV 规则

- 每行表示一个词条。
- `word` 和 `meaning` 必须填写。
- 空行会被忽略。
- 字段包含英文逗号时，需要使用英文双引号包裹。
- 字段包含双引号时，需要写成两个双引号。
- 同一个 CSV 中重复的单词会被跳过，重复判断不区分大小写。

## 常见错误

导入时，应用会提示无效行。

| 问题 | 示例 |
| --- | --- |
| 单词为空 | `,苹果,/ˈæpəl/,I ate an apple.,noun,` |
| 释义为空 | `apple,,/ˈæpəl/,I ate an apple.,noun,` |
| 单词重复 | `apple,苹果` 后再次出现 `Apple,苹果` |

## 发音音频

当 `audio` 字段指向可播放的文件或 URI 时，Take Word 会优先播放该音频。无法播放或没有填写时，会使用 Android TextToSpeech 兜底。

请勿分发未授权的真人发音文件。
