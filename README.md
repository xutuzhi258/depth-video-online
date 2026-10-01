# 深度视频转换器 · 在线版

打开即可用的浏览器端视频效果工具，**视频全程不上传服务器**，全部在你的设备本地推理。

## 功能

- **面部 478 点云** — MediaPipe FaceLandmarker（含虹膜），浏览器 GPU/CPU 实时推理
- **人体姿态骨架** — MediaPipe PoseLandmarker（33 关键点）
- 拖拽上传 / 摄像头实时预览
- 绘制选项：显示点号、连线、保留原画面、镜面镜像
- 导出为 WebM，可**混入原视频音轨**（保留原声）

打开 → 选视频 → 选效果 → 「开始处理并导出」→ 下载。

## 与本地版的区别

在线版是纯前端方案，受浏览器能力限制，**深度估计（Depth-Anything-V2）无法在浏览器内运行**，
因此灰度深度图、深度+姿态、全部叠加这些模式属于本地版功能。

本地版（Flask + PyTorch + MediaPipe 双环境、ffmpeg 合成、保留原声导出）见
[`xutuzhi258/depth-video-tool`](https://github.com/xutuzhi258/depth-video-tool)，
需本地安装运行，适合需要深度图与音视频合成的场景。

## 在线体验

> https://xutuzhi258.github.io/depth-video-online/

## 技术栈

单文件 `index.html`，无任何构建步骤。运行时从 CDN 动态加载：

- `@mediapipe/tasks-vision@0.10.14`（jsDelivr）
- face_landmarker / pose_landmarker `.task` 模型（storage.googleapis.com）

导出使用 `canvas.captureStream()` + `MediaRecorder`（VP9/Opus）。

## 兼容性与注意

- 建议使用较新的 Chrome / Edge / Safari（支持 WebAssembly SIMD 与 MediaPipe GPU delegate）。
- GPU 委托不可用时会自动回退到 CPU。
- 导出为实时录制，耗时约等于「视频时长 × 所选效果数」。
- 私有仓库 GitHub Pages 需要付费计划；本仓库为公开，Pages 免费可用。
