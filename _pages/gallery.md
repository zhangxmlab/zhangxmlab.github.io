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
    <title>校园风光画廊</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            color: #333;
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            width: 100%;
            margin: 0 auto;
            padding: 20px;
        }
        
        .gallery-container {
            position: relative;
            width: 100%;
            max-width: 900px;
            margin: 0 auto;
            box-shadow: 0 10px 30px rgba(0, 0, 100, 0.15);
            border-radius: 15px;
            overflow: hidden;
            background-color: white;
        }
        
        .image-container {
            position: relative;
            width: 100%;
            height: 500px;
            overflow: hidden;
        }
        
        .image-slide {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0;
            transition: opacity 0.8s ease-in-out;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #f8fafc;
        }
        
        .image-slide.active {
            opacity: 1;
        }
        
        .image-slide img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        
        .image-caption {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
            color: white;
            padding: 25px 20px 15px;
            text-align: center;
        }
        
        .image-caption h3 {
            font-size: 1.5rem;
            margin-bottom: 5px;
        }
        
        .image-caption p {
            font-size: 1rem;
            opacity: 0.9;
            max-width: 700px;
            margin: 0 auto;
        }
        
        .nav-button {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background-color: rgba(255, 255, 255, 0.9);
            border: none;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
            color: #2c5282;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            z-index: 10;
        }
        
        .nav-button:hover {
            background-color: #2c5282;
            color: white;
            transform: translateY(-50%) scale(1.1);
        }
        
        .nav-button:active {
            transform: translateY(-50%) scale(0.95);
        }
        
        .prev-button {
            left: 20px;
        }
        
        .next-button {
            right: 20px;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .image-container {
                height: 400px;
            }
            
            .nav-button {
                width: 50px;
                height: 50px;
                font-size: 1.5rem;
            }
            
            .prev-button {
                left: 10px;
            }
            
            .next-button {
                right: 10px;
            }
            
            .image-caption {
                padding: 20px 15px 10px;
            }
            
            .image-caption h3 {
                font-size: 1.3rem;
            }
        }
        
        @media (max-width: 480px) {
            .image-container {
                height: 300px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="gallery-container">
            <div class="image-container">
                <!-- 图片幻灯片将通过JavaScript动态生成 -->
            </div>
            
            <button class="nav-button prev-button" aria-label="上一张图片">
                <i class="fas fa-chevron-left"></i>
            </button>
            <button class="nav-button next-button" aria-label="下一张图片">
                <i class="fas fa-chevron-right"></i>
            </button>
            
            <div class="image-caption">
                <!-- 图片标题将通过JavaScript动态生成 -->
            </div>
        </div>
    </div>

    <script>
        // 校园图片数据
        const campusImages = [
            {
                id: 1,
                url: "https://images.unsplash.com/photo-1523050854058-8df90110c9f1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
                title: "校园正门",
                description: "学校正门入口，庄严大气，绿树成荫，是学校的标志性建筑之一。"
            },
            {
                id: 2,
                url: "https://images.unsplash.com/photo-1562774053-701939374585?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
                title: "图书馆大楼",
                description: "现代化图书馆，藏书丰富，是学生们学习研究的重要场所。"
            },
            {
                id: 3,
                url: "https://images.unsplash.com/photo-1541339907198-e08756dedf3f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
                title: "教学楼",
                description: "现代化的教学楼，设施齐全，为师生提供了优良的教学环境。"
            },
            {
                id: 4,
                url: "https://images.unsplash.com/photo-1523580494863-6f3031224c94?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
                title: "实验中心",
                description: "先进的实验中心，配备各类实验设备，支持学生进行科学研究和实践。"
            },
            {
                id: 5,
                url: "https://images.unsplash.com/photo-1524178234883-043d5c3f3cf4?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
                title: "学生活动中心",
                description: "学生活动中心，各类社团活动、文艺演出和学术讲座在这里举行。"
            },
            {
                id: 6,
                url: "https://images.unsplash.com/photo-1576495199012-8b4b2c6a1d4c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
                title: "校园操场",
                description: "宽敞的操场，是学生体育锻炼、举办运动会和日常活动的主要场所。"
            },
            {
                id: 7,
                url: "https://images.unsplash.com/photo-1588072432836-e10032774350?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
                title: "学生宿舍",
                description: "舒适的学生宿舍区，绿树环绕，为学生提供了良好的生活环境。"
            },
            {
                id: 8,
                url: "https://images.unsplash.com/photo-1542744095-fcf48d80b0fd?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
                title: "校园湖景",
                description: "校园内的湖泊，风景优美，是师生休闲散步、放松心情的好去处。"
            }
        ];

        // DOM元素
        const imageContainer = document.querySelector('.image-container');
        const captionContainer = document.querySelector('.image-caption');
        const prevButton = document.querySelector('.prev-button');
        const nextButton = document.querySelector('.next-button');
        
        let currentIndex = 0;
        
        // 初始化画廊
        function initGallery() {
            // 创建图片幻灯片
            campusImages.forEach((image, index) => {
                // 创建主图片幻灯片
                const slide = document.createElement('div');
                slide.className = `image-slide ${index === 0 ? 'active' : ''}`;
                slide.dataset.index = index;
                
                const img = document.createElement('img');
                img.src = image.url;
                img.alt = image.title;
                
                slide.appendChild(img);
                imageContainer.appendChild(slide);
            });
            
            // 设置第一张图片的标题
            updateCaption();
            
            // 添加事件监听器
            prevButton.addEventListener('click', showPrevImage);
            nextButton.addEventListener('click', showNextImage);
            
            // 键盘导航
            document.addEventListener('keydown', handleKeyDown);
            
            // 触摸滑动支持
            let touchStartX = 0;
            let touchEndX = 0;
            
            imageContainer.addEventListener('touchstart', e => {
                touchStartX = e.changedTouches[0].screenX;
            });
            
            imageContainer.addEventListener('touchend', e => {
                touchEndX = e.changedTouches[0].screenX;
                handleSwipe();
            });
        }
        
        // 显示上一张图片
        function showPrevImage() {
            currentIndex = (currentIndex - 1 + campusImages.length) % campusImages.length;
            updateGallery();
        }
        
        // 显示下一张图片
        function showNextImage() {
            currentIndex = (currentIndex + 1) % campusImages.length;
            updateGallery();
        }
        
        // 跳转到指定图片
        function goToImage(index) {
            currentIndex = index;
            updateGallery();
        }
        
        // 更新画廊
        function updateGallery() {
            // 更新主图片
            const slides = document.querySelectorAll('.image-slide');
            slides.forEach(slide => {
                slide.classList.remove('active');
            });
            
            slides[currentIndex].classList.add('active');
            
            // 更新标题
            updateCaption();
        }
        
        // 更新图片标题
        function updateCaption() {
            const currentImage = campusImages[currentIndex];
            captionContainer.innerHTML = `
                <h3>${currentImage.title}</h3>
                <p>${currentImage.description}</p>
            `;
        }
        
        // 处理键盘事件
        function handleKeyDown(e) {
            if (e.key === 'ArrowLeft') {
                showPrevImage();
            } else if (e.key === 'ArrowRight') {
                showNextImage();
            }
        }
        
        // 处理触摸滑动
        function handleSwipe() {
            const swipeThreshold = 50; // 最小滑动距离
            
            if (touchStartX - touchEndX > swipeThreshold) {
                // 向左滑动，下一张
                showNextImage();
            } else if (touchEndX - touchStartX > swipeThreshold) {
                // 向右滑动，上一张
                showPrevImage();
            }
        }
        
        // 自动轮播功能（可选）
        let autoSlideInterval;
        
        function startAutoSlide() {
            autoSlideInterval = setInterval(showNextImage, 5000); // 每5秒切换
        }
        
        function stopAutoSlide() {
            clearInterval(autoSlideInterval);
        }
        
        // 当鼠标悬停在画廊上时停止自动轮播
        document.querySelector('.gallery-container').addEventListener('mouseenter', stopAutoSlide);
        document.querySelector('.gallery-container').addEventListener('mouseleave', startAutoSlide);
        
        // 初始化画廊并开始自动轮播
        window.addEventListener('DOMContentLoaded', () => {
            initGallery();
            startAutoSlide();
        });
    </script>
</body>
</html>
