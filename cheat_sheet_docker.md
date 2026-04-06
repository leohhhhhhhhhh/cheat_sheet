#  Docker & WSL 

##  一、 WSL 系統操作

- **開啟 WSL**: `wsl`
- **關閉當前視窗**: `exit`
- **徹底關閉 WSL**: `wsl --shutdown`

---

##  二、 Docker 映像檔 (Image) 管理

- **下載最新公開 Image**: `docker pull ubuntu`
- **看看自己有的 Image**: `docker image ls`
- **編譯自己的 Image**: `docker build -t 專案名稱:版本號 .`
  - *最後的 `.` 代表在目前資料夾尋找 Dockerfile*

---

##  三、 Docker 容器 (Container) 操作

### 1. 創建並跑起來
- `docker run -it --name 容器名 ubuntu bash`
  - *`docker run` 是一個每次都重新創建新的 container 的指令*

### 2. 離開與查看狀態
- **暫停退出**: `exit` 
  - *進去後會看到EX. `root@a8a370441a15:/#`，其中 @ 後面是 Container ID*
- **退出後看所有容器狀態**: `docker ps -a`

### 3. 重啟現有容器 (要重啟而不是重新創建)
- **啟動容器**: `docker start <ContainerID或名稱>`
- **重新鑽進去操作**: `docker exec -it <ContainerID或名稱> bash`

---

##  四、 Build & Run 實戰流程
1. **編譯 Image**:
   `docker build -t 專案名稱:版本號 .`
2. **執行並進入互動模式**:
   `docker run -it --name 容器名 專案名稱:版本號 bash`
3. **從容器抓檔案出來 (拿成果)**:
   `docker cp 容器名:/app/結果.png ./本地路徑.png`
4. **指定要開啟哪個dockerfile**:
   `docker build -f 哪個Dockerfile -t 專案名稱:版本號 .`
---

##  五、 Python OpenCV Dockerfile 模板 (D槽專用)
*解決 OpenCV 在 Docker 噴錯的公式化寫法*

```dockerfile
# 1. 基礎環境
FROM python:3.9-slim
WORKDIR /app

# 2. 修正 OpenCV 報錯必備 (libGL 救命藥水)
RUN apt-get update && apt-get install -y \
    libglib2.0-0 \
    libgl1-mesa-glx \
    && rm -rf /var/lib/apt/lists/*

# 3. 安裝 Python 套件
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 4. 搬入原始碼與執行
COPY . .
CMD ["python", "app.py"]

```
---

##  六、 進階管理
- **停止容器**: `docker stop <ID>`
- **刪除沒用的垃圾 (省空間)**: `docker system prune -a`

---

###  工程師隨筆：這需要「背」嗎？
**不需要死背，但要「理解」！**
身為資工系的學生，你的腦袋是用來解演算法的。
1. **邏輯重要**：懂 `run` (開新房) 跟 `exec` (回舊房) 的差別。
2. **參數查表**：忘記 `-it` 或是 `apt` 指令就回來翻這份 `.md`。
3. **肌肉記憶**：多 build 幾次專案，你的手指會跑得比大腦快。
