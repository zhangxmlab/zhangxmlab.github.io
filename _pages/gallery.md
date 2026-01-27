---
layout: archive
title: "Gallery"
permalink: /gallery/
author_profile: true
---

Campus Scenery
=====
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>图片浏览</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        .gallery-container {
            position: relative;
            width: 100%;
            max-width: 900px;
            margin: 0 auto;
            overflow: hidden;
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
            padding: 20px;
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
        
        .prev-button {
            left: 20px;
        }
        
        .next-button {
            right: 20px;
        }
        
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
        }
        
        @media (max-width: 480px) {
            .image-container {
                height: 300px;
            }
        }
    </style>
</head>
<body>
    <div class="gallery-container">
        <div class="image-container"></div>
        
        <button class="nav-button prev-button" aria-label="上一张图片">
            <i class="fas fa-chevron-left"></i>
        </button>
        <button class="nav-button next-button" aria-label="下一张图片">
            <i class="fas fa-chevron-right"></i>
        </button>
        
        <div class="image-caption"></div>
    </div>

    <script>
        // 图片数据
        const images = [
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
            images.forEach((image, index) => {
                const slide = document.createElement('div');
                slide.className = `image-slide ${index === 0 ? 'active' : ''}`;
                
                const img = document.createElement('img');
                img.src = image.url;
                img.alt = image.title;
                
                slide.appendChild(img);
                imageContainer.appendChild(slide);
            });
            
            updateCaption();
            
            // 事件监听器
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
            
            // 自动轮播
            startAutoSlide();
        }
        
        function showPrevImage() {
            currentIndex = (currentIndex - 1 + images.length) % images.length;
            updateGallery();
        }
        
        function showNextImage() {
            currentIndex = (currentIndex + 1) % images.length;
            updateGallery();
        }
        
        function updateGallery() {
            const slides = document.querySelectorAll('.image-slide');
            slides.forEach(slide => slide.classList.remove('active'));
            slides[currentIndex].classList.add('active');
            updateCaption();
        }
        
        function updateCaption() {
            const currentImage = images[currentIndex];
            captionContainer.innerHTML = `
                <h3>${currentImage.title}</h3>
                <p>${currentImage.description}</p>
            `;
        }
        
        function handleKeyDown(e) {
            if (e.key === 'ArrowLeft') showPrevImage();
            else if (e.key === 'ArrowRight') showNextImage();
        }
        
        function handleSwipe() {
            const swipeThreshold = 50;
            let touchStartX = 0;
            let touchEndX = 0;
            
            if (touchStartX - touchEndX > swipeThreshold) {
                showNextImage();
            } else if (touchEndX - touchStartX > swipeThreshold) {
                showPrevImage();
            }
        }
        
        let autoSlideInterval;
        function startAutoSlide() {
            autoSlideInterval = setInterval(showNextImage, 5000);
        }
        
        function stopAutoSlide() {
            clearInterval(autoSlideInterval);
        }
        
        document.querySelector('.gallery-container').addEventListener('mouseenter', stopAutoSlide);
        document.querySelector('.gallery-container').addEventListener('mouseleave', startAutoSlide);
        
        window.addEventListener('DOMContentLoaded', initGallery);
    </script>
</body>
</html>
          
