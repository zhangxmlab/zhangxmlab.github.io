---
layout: archive
title: "Gallery"
permalink: /gallery/
author_profile: true
---

 <!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>多图浏览系统 - 左右切换</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 1400px;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }

        header {
            background: linear-gradient(to right, #2c3e50, #4a6491);
            color: white;
            padding: 25px;
            text-align: center;
            position: relative;
        }

        header h1 {
            font-size: 2.4rem;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }

        header h1 i {
            font-size: 2.8rem;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
            font-weight: 300;
        }

        .main-content {
            display: flex;
            min-height: 600px;
        }

        /* 图片展示区域 */
        .image-display-section {
            flex: 3;
            background: #000;
            position: relative;
            overflow: hidden;
        }

        .image-viewer {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        .image-slide {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0;
            transition: opacity 0.5s ease, transform 0.5s ease;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 40px;
        }

        .image-slide.active {
            opacity: 1;
            transform: scale(1);
        }

        .image-slide img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
        }

        /* 导航控制 */
        .navigation-controls {
            position: absolute;
            top: 50%;
            left: 0;
            right: 0;
            transform: translateY(-50%);
            display: flex;
            justify-content: space-between;
            padding: 0 30px;
            z-index: 100;
        }

        .nav-btn {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255, 255, 255, 0.3);
            color: white;
            font-size: 28px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .nav-btn:hover:not(:disabled) {
            background: rgba(255, 255, 255, 0.25);
            transform: scale(1.1);
            border-color: rgba(255, 255, 255, 0.5);
            box-shadow: 0 5px 20px rgba(255, 255, 255, 0.2);
        }

        .nav-btn:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }

        /* 底部信息栏 */
        .image-info-bar {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
            color: white;
            padding: 20px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .image-counter {
            font-size: 1.4rem;
            font-weight: bold;
            background: rgba(255, 255, 255, 0.1);
            padding: 8px 20px;
            border-radius: 30px;
            backdrop-filter: blur(5px);
        }

        .image-name {
            font-size: 1.2rem;
            max-width: 300px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        /* 缩略图区域 */
        .thumbnail-section {
            flex: 1;
            background: #1a1a1a;
            padding: 25px;
            display: flex;
            flex-direction: column;
            max-height: 600px;
        }

        .thumbnail-section h3 {
            color: white;
            margin-bottom: 20px;
            font-size: 1.4rem;
            display: flex;
            align-items: center;
            gap: 10px;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(255, 255, 255, 0.1);
        }

        .thumbnail-container {
            flex: 1;
            overflow-y: auto;
            padding-right: 10px;
        }

        /* 自定义滚动条 */
        .thumbnail-container::-webkit-scrollbar {
            width: 8px;
        }

        .thumbnail-container::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 4px;
        }

        .thumbnail-container::-webkit-scrollbar-thumb {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 4px;
        }

        .thumbnail-container::-webkit-scrollbar-thumb:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .thumbnail-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }

        .thumbnail-item {
            width: 100%;
            height: 150px;
            border-radius: 10px;
            overflow: hidden;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 3px solid transparent;
            position: relative;
        }

        .thumbnail-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }

        .thumbnail-item.active {
            border-color: #667eea;
            box-shadow: 0 0 20px rgba(102, 126, 234, 0.5);
        }

        .thumbnail-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.3s ease;
        }

        .thumbnail-item:hover img {
            transform: scale(1.05);
        }

        .thumbnail-index {
            position: absolute;
            top: 10px;
            left: 10px;
            background: rgba(0, 0, 0, 0.7);
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
            font-size: 0.9rem;
        }

        /* 控制面板 */
        .controls-panel {
            background: #2a2a2a;
            padding: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .control-buttons {
            display: flex;
            gap: 15px;
        }

        .control-btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 8px;
            background: linear-gradient(to right, #667eea, #764ba2);
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
            font-size: 1rem;
        }

        .control-btn:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .control-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .control-btn.secondary {
            background: linear-gradient(to right, #4CAF50, #45a049);
        }

        .control-btn.danger {
            background: linear-gradient(to right, #ff416c, #ff4b2b);
        }

        /* 键盘快捷键提示 */
        .keyboard-hints {
            background: rgba(255, 255, 255, 0.05);
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
        }

        .keyboard-hints h4 {
            color: white;
            margin-bottom: 10px;
            font-size: 1rem;
        }

        .hint-items {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .hint-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 8px 15px;
            border-radius: 6px;
            font-size: 0.9rem;
            color: #ccc;
        }

        .hint-item kbd {
            background: rgba(0, 0, 0, 0.3);
            padding: 4px 8px;
            border-radius: 4px;
            font-family: monospace;
            margin-right: 5px;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        footer {
            background: #2c3e50;
            color: white;
            text-align: center;
            padding: 20px;
            font-size: 0.9rem;
            opacity: 0.9;
        }

        /* 响应式设计 */
        @media (max-width: 1024px) {
            .main-content {
                flex-direction: column;
                min-height: auto;
            }
            
            .image-display-section {
                height: 500px;
            }
            
            .thumbnail-section {
                max-height: 400px;
            }
            
            .thumbnail-grid {
                grid-template-columns: repeat(4, 1fr);
            }
        }

        @media (max-width: 768px) {
            .container {
                border-radius: 15px;
            }
            
            header h1 {
                font-size: 1.8rem;
            }
            
            .nav-btn {
                width: 60px;
                height: 60px;
                font-size: 24px;
            }
            
            .thumbnail-grid {
                grid-template-columns: repeat(3, 1fr);
            }
            
            .thumbnail-item {
                height: 120px;
            }
        }

        @media (max-width: 480px) {
            .thumbnail-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .image-info-bar {
                flex-direction: column;
                gap: 10px;
                text-align: center;
            }
            
            .control-buttons {
                flex-direction: column;
            }
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-images"></i> 多图浏览系统</h1>
            <p class="subtitle">支持左右切换浏览，点击缩略图快速导航</p>
        </header>

        <div class="main-content">
            <!-- 左侧：图片展示区域 -->
            <div class="image-display-section">
                <div class="image-viewer" id="imageViewer">
                    <!-- 图片将通过JavaScript动态插入 -->
                    <div class="image-slide placeholder">
                        <div style="text-align: center; color: white;">
                            <i class="fas fa-image" style="font-size: 5rem; opacity: 0.3; margin-bottom: 20px;"></i>
                            <p style="font-size: 1.2rem;">请选择要浏览的图片</p>
                        </div>
                    </div>
                </div>

                <!-- 导航按钮 -->
                <div class="navigation-controls">
                    <button class="nav-btn" id="prevBtn" disabled>
                        <i class="fas fa-chevron-left"></i>
                    </button>
                    <button class="nav-btn" id="nextBtn" disabled>
                        <i class="fas fa-chevron-right"></i>
                    </button>
                </div>

                <!-- 底部信息栏 -->
                <div class="image-info-bar">
                    <div class="image-counter" id="imageCounter">0 / 0</div>
                    <div class="image-name" id="imageName">未选择图片</div>
                </div>
            </div>

            <!-- 右侧：缩略图和控制面板 -->
            <div class="thumbnail-section">
                <h3><i class="fas fa-th"></i> 图片列表</h3>
                
                <div class="thumbnail-container" id="thumbnailContainer">
                    <div class="thumbnail-grid" id="thumbnailGrid">
                        <!-- 缩略图将通过JavaScript动态插入 -->
                    </div>
                </div>

                <div class="controls-panel">
                    <div class="control-buttons">
                        <button class="control-btn" id="addBtn">
                            <i class="fas fa-folder-open"></i> 添加图片
                        </button>
                        <button class="control-btn secondary" id="autoPlayBtn">
                            <i class="fas fa-play"></i> 自动播放
                        </button>
                        <button class="control-btn danger" id="clearBtn" disabled>
                            <i class="fas fa-trash"></i> 清空
                        </button>
                    </div>

                    <div class="keyboard-hints">
                        <h4><i class="fas fa-keyboard"></i> 键盘快捷键</h4>
                        <div class="hint-items">
                            <div class="hint-item"><kbd>←</kbd> 上一张</div>
                            <div class="hint-item"><kbd>→</kbd> 下一张</div>
                            <div class="hint-item"><kbd>空格</kbd> 播放/暂停</div>
                            <div class="hint-item"><kbd>ESC</kbd> 退出全屏</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <footer>
            <p>© 2023 多图浏览系统 | 使用左右箭头切换图片 | 支持拖拽上传</p>
        </footer>
    </div>

    <!-- 隐藏的文件输入 -->
    <input type="file" id="fileInput" accept="image/*" multiple style="display: none;">

    <script>
        // 图片数据管理
        class ImageGallery {
            constructor() {
                this.images = [];
                this.currentIndex = -1;
                this.isAutoPlaying = false;
                this.autoPlayInterval = null;
                this.autoPlayDelay = 3000; // 3秒自动切换
                
                // 初始化DOM元素
                this.initElements();
                // 绑定事件
                this.bindEvents();
                // 加载示例图片
                this.loadSampleImages();
            }

            initElements() {
                this.imageViewer = document.getElementById('imageViewer');
                this.thumbnailGrid = document.getElementById('thumbnailGrid');
                this.prevBtn = document.getElementById('prevBtn');
                this.nextBtn = document.getElementById('nextBtn');
                this.imageCounter = document.getElementById('imageCounter');
                this.imageName = document.getElementById('imageName');
                this.addBtn = document.getElementById('addBtn');
                this.clearBtn = document.getElementById('clearBtn');
                this.autoPlayBtn = document.getElementById('autoPlayBtn');
                this.fileInput = document.getElementById('fileInput');
            }

            bindEvents() {
                // 按钮事件
                this.prevBtn.addEventListener('click', () => this.prevImage());
                this.nextBtn.addEventListener('click', () => this.nextImage());
                this.addBtn.addEventListener('click', () => this.fileInput.click());
                this.clearBtn.addEventListener('click', () => this.clearAll());
                this.autoPlayBtn.addEventListener('click', () => this.toggleAutoPlay());
                
                // 文件选择事件
                this.fileInput.addEventListener('change', (e) => this.handleFiles(e.target.files));
                
                // 拖拽上传
                document.addEventListener('dragover', (e) => {
                    e.preventDefault();
                    document.body.style.backgroundColor = 'rgba(102, 126, 234, 0.1)';
                });
                
                document.addEventListener('dragleave', () => {
                    document.body.style.backgroundColor = '';
                });
                
                document.addEventListener('drop', (e) => {
                    e.preventDefault();
                    document.body.style.backgroundColor = '';
                    if (e.dataTransfer.files.length) {
                        this.handleFiles(e.dataTransfer.files);
                    }
                });
                
                // 键盘快捷键
                document.addEventListener('keydown', (e) => {
                    if (this.images.length === 0) return;
                    
                    switch(e.key) {
                        case 'ArrowLeft':
                            e.preventDefault();
                            this.prevImage();
                            break;
                        case 'ArrowRight':
                            e.preventDefault();
                            this.nextImage();
                            break;
                        case ' ':
                            e.preventDefault();
                            this.toggleAutoPlay();
                            break;
                        case 'Escape':
                            if (document.fullscreenElement) {
                                document.exitFullscreen();
                            }
                            break;
                    }
                });
                
                // 全屏切换
                this.imageViewer.addEventListener('dblclick', () => {
                    if (!document.fullscreenElement) {
                        this.imageViewer.requestFullscreen().catch(console.log);
                    } else {
                        document.exitFullscreen();
                    }
                });
            }

            // 加载示例图片
            async loadSampleImages() {
                const sampleImages = [
                    'https://images.unsplash.com/photo-1506744038136-46273834b3fb',
                    'https://images.unsplash.com/photo-1519681393784-d120267933ba',
                    'https://images.unsplash.com/photo-1518834103327-0d0b5c812a0c',
                    'https://images.unsplash.com/photo-1439066615861-d1af74d74000',
                    'https://images.unsplash.com/photo-1426604966848-d7adac402bff',
                    'https://images.unsplash.com/photo-1470071459604-3b5ec3a7fe05'
                ];
                
                // 添加示例图片
                for (const imgUrl of sampleImages) {
                    try {
                        const response = await fetch(imgUrl + '?w=800&h=600&fit=crop');
                        const blob = await response.blob();
                        const imageUrl = URL.createObjectURL(blob);
                        this.images.push({
                            url: imageUrl,
                            name: `示例图片 ${this.images.length + 1}`,
                            size: (blob.size / 1024 / 1024).toFixed(2) + ' MB'
                        });
                    } catch (error) {
                        console.log('加载示例图片失败:', error);
                    }
                }
                
                if (this.images.length > 0) {
                    this.displayImage(0);
                }
            }

            // 处理上传的文件
            handleFiles(files) {
                const validFiles = Array.from(files).filter(file => 
                    file.type.startsWith('image/')
                );
                
                if (validFiles.length === 0) {
                    this.showMessage('请选择有效的图片文件！', 'error');
                    return;
                }
                
                // 限制最多50张图片
                if (this.images.length + validFiles.length > 50) {
                    this.showMessage('最多只能添加50张图片！', 'error');
                    return;
                }
                
                validFiles.forEach(file => {
                    const imageUrl = URL.createObjectURL(file);
                    this.images.push({
                        url: imageUrl,
                        name: file.name.length > 30 ? file.name.substring(0, 30) + '...' : file.name,
                        size: (file.size / 1024 / 1024).toFixed(2) + ' MB',
                        originalName: file.name
                    });
                });
                
                this.showMessage(`成功添加 ${validFiles.length} 张图片！`, 'success');
                
                // 如果是第一次添加图片，显示第一张
                if (this.currentIndex === -1 && this.images.length > 0) {
                    this.displayImage(0);
                }
                
                this.updateUI();
            }

            // 显示图片
            displayImage(index) {
                if (this.images.length === 0) {
                    this.showPlaceholder();
                    return;
                }
                
                // 确保索引在有效范围内
                this.currentIndex = (index + this.images.length) % this.images.length;
                
                // 清空现有图片
                this.imageViewer.innerHTML = '';
                
                // 创建图片元素
                const imgSlide = document.createElement('div');
                imgSlide.className = 'image-slide active';
                
                const img = document.createElement('img');
                img.src = this.images[this.currentIndex].url;
                img.alt = this.images[this.currentIndex].name;
                img.onload = () => {
                    // 图片加载完成后的处理
                };
                
                imgSlide.appendChild(img);
                this.imageViewer.appendChild(imgSlide);
                
                // 更新信息
                this.updateInfo();
                // 更新缩略图选中状态
                this.updateThumbnails();
                // 更新按钮状态
                this.updateButtons();
            }

            // 上一张图片
            prevImage() {
                if (this.images.length > 1) {
                    this.displayImage(this.currentIndex - 1);
                }
            }

            // 下一张图片
            nextImage() {
                if (this.images.length > 1) {
                    this.displayImage(this.currentIndex + 1);
                }
            }

            // 切换自动播放
            toggleAutoPlay() {
                if (this.isAutoPlaying) {
                    this.stopAutoPlay();
                } else {
                    this.startAutoPlay();
                }
            }

            // 开始自动播放
            startAutoPlay() {
                if (this.images.length < 2) return;
                
                this.isAutoPlaying = true;
                this.autoPlayBtn.innerHTML = '<i class="fas fa-pause"></i> 停止播放';
                this.autoPlayBtn.classList.remove('secondary');
                this.autoPlayBtn.classList.add('danger');
                
                this.autoPlayInterval = setInterval(() => {
                    this.nextImage();
                }, this.autoPlayDelay);
            }

            // 停止自动播放
            stopAutoPlay() {
                this.isAutoPlaying = false;
                clearInterval(this.autoPlayInterval);
                this.autoPlayBtn.innerHTML = '<i class="fas fa-play"></i> 自动播放';
                this.autoPlayBtn.classList.remove('danger');
                this.autoPlayBtn.classList.add('secondary');
            }

            // 清空所有图片
            clearAll() {
                if (this.images.length === 0) return;
                
                if (confirm('确定要清空所有图片吗？此操作不可撤销。')) {
                    // 停止自动播放
                    if (this.isAutoPlaying) {
                        this.stopAutoPlay();
                    }
                    
                    // 释放所有对象URL
                    this.images.forEach(image => {
                        URL.revokeObjectURL(image.url);
                    });
                    
                    // 清空数组
                    this.images = [];
                    this.currentIndex = -1;
                    
                    // 更新界面
                    this.showPlaceholder();
                    this.updateUI();
                    this.showMessage('已清空所有图片', 'info');
                }
            }

            // 显示占位符
            showPlaceholder() {
                this.imageViewer.innerHTML = `
                    <div class="image-slide placeholder" style="opacity: 1;">
                        <div style="text-align: center; color: white;">
                            <i class="fas fa-image" style="font-size: 5rem; opacity: 0.3; margin-bottom: 20px;"></i>
                            <p style="font-size: 1.2rem;">请添加要浏览的图片</p>
                            <p style="opacity: 0.7; margin-top: 10px;">
                                点击"添加图片"按钮或拖拽图片到此处
                            </p>
                        </div>
                    </div>
                `;
                
                this.imageCounter.textContent = '0 / 0';
                this.imageName.textContent = '未选择图片';
            }

            // 更新信息显示
            updateInfo() {
                const total = this.images.length;
                const current = this.currentIndex + 1;
                this.imageCounter.textContent = `${current} / ${total}`;
                this.imageName.textContent = `${this.images[this.currentIndex].name}`;
            }

            // 更新缩略图
            updateThumbnails() {
                this.thumbnailGrid.innerHTML = '';
                
                if (this.images.length === 0) {
                    this.thumbnailGrid.innerHTML = `
                        <div style="grid-column: 1 / -1; text-align: center; color: #888; padding: 40px;">
                            <i class="fas fa-image" style="font-size: 3rem; opacity: 0.3; margin-bottom: 15px;"></i>
                            <p>暂无图片</p>
                        </div>
                    `;
                    return;
                }
                
                this.images.forEach((image, index) => {
                    const thumbnail = document.createElement('div');
                    thumbnail.className = `thumbnail-item ${index === this.currentIndex ? 'active' : ''}`;
                    thumbnail.innerHTML = `
                        <div class="thumbnail-index">${index + 1}</div>
                        <img src="${image.url}" alt="${image.name}">
                    `;
                    
                    thumbnail.addEventListener('click', () => {
                        this.displayImage(index);
                    });
                    
                    this.thumbnailGrid.appendChild(thumbnail);
                });
            }

            // 更新按钮状态
            updateButtons() {
                const hasImages = this.images.length > 0;
                const hasMultipleImages = this.images.length > 1;
                
                this.prevBtn.disabled = !hasMultipleImages;
                this.nextBtn.disabled = !hasMultipleImages;
                this.clearBtn.disabled = !hasImages;
                this.autoPlayBtn.disabled = !hasMultipleImages;
            }

            // 更新UI
            updateUI() {
                this.updateInfo();
                this.updateThumbnails();
                this.updateButtons();
            }

            // 显示消息
            showMessage(message, type = 'info') {
                // 移除现有的消息
                const existingMsg = document.querySelector('.message-toast');
                if (existingMsg) existingMsg.remove();
                
                // 创建消息元素
                const msgElement = document.createElement('div');
                msgElement.className = `message-toast ${type}`;
                msgElement.innerHTML = `
                    <i class="fas fa-${type === 'error' ? 'exclamation-circle' : type === 'success' ? 'check-circle' : 'info-circle'}"></i>
                    <span>${message}</span>
                `;
                
                // 添加样式
                msgElement.style.cssText = `
                    position: fixed;
                    top: 20px;
                    right: 20px;
                    background: ${type === 'error' ? '#ff4b2b' : type === 'success' ? '#4CAF50' : '#2196F3'};
                    color: white;
                    padding: 15px 25px;
                    border-radius: 10px;
                    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
                    display: flex;
                    align-items: center;
                    gap: 10px;
                    z-index: 1000;
                    animation: slideIn 0.3s ease;
                `;
                
                // 添加动画
                const style = document.createElement('style');
                style.textContent = `
                    @keyframes slideIn {
                        from { transform: translateX(100%); opacity: 0; }
                        to { transform: translateX(0); opacity: 1; }
                    }
                `;
                document.head.appendChild(style);
                
                document.body.appendChild(msgElement);
                
                // 3秒后自动移除
                setTimeout(() => {
                    if (msgElement.parentNode) {
                        msgElement.style.animation = 'slideOut 0.3s ease';
                        setTimeout(() => msgElement.remove(), 300);
                    }
                }, 3000);
            }
        }

        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', () => {
            window.imageGallery = new ImageGallery();
        });
    </script>
</body>
</html>
