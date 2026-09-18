# Sleep-Talk-Emotion-Analysis
# Sleep AI Voice Monitor

睡眠語音監測系統
功能：

* VAD / Volume 雙方案錄音
* 自動保存睡眠語音
* SQLite管理錄音資料
* Whisper語音轉文字
* Qwen3本地模型生成睡眠分析報告

## 目錄結構

sleep_ai/
│
├── main_vad.py          # Silero VAD監測入口
├── main_volume.py       # 音量閾值監測入口
│
├── vad_monitor.py       # VAD聲音檢測
├── volume_monitor.py    # Volume聲音檢測
├── recorder.py          # 保存wav並寫入資料庫
├── database.py          # SQLite資料管理
│
├── transcript.py        # Whisper轉文字
├── llm_analysis.py      # Qwen3 AI分析
├── pipeline.py          # 一鍵執行分析流程
│
├── recordings/          # 原始wav錄音
├── recordings_txt/      # 文字和AI報告
└── sleep.db             # SQLite資料庫
# Sleep AI 使用指南

## 1. 晚上開始監測

推薦VAD版本：

```bash
python main_vad.py
```

或者音量版本：

```bash
python main_volume.py
```

運行後等待即可。

錄音保存：

```
recordings/
```

資料同步保存：

```
sleep.db
```

## 2. 早上生成分析

停止錄音後執行：

```bash
python pipeline.py
```

自動完成：

```
wav
 ↓
Whisper轉文字
 ↓
更新sleep.db
 ↓
生成transcript
 ↓
Qwen分析
 ↓
生成AI報告
```

## 3. 查看結果

文字記錄：

```
recordings_txt/
xxx_transcript.txt
```

AI分析：

```
recordings_txt/
xxx_sleep_AI_report.txt
```

## 4. 啟動Qwen

如果AI分析報錯：

先開：

```bash
ollama serve
```

確認：

```bash
ollama list
```

存在：

```
qwen3:8b
```

## 5. 查看資料庫

進入：

```bash
sqlite3 sleep.db
```

查看：

```sql
select * from records;
```

退出：

```sql
.quit
```

## 6. 完整流程

晚上：

```bash
python main_vad.py
```

早上：

```bash
python pipeline.py
```

查看：

```
recordings_txt/
```

完成。
