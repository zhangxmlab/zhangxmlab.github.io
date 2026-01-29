---
layout: archive
title: "Gallery"
permalink: /gallery/
author_profile: true
---

Campus Scenery
=====
<div class="gallery">
    <div class="gallery__container">
        <div class="gallery__slides">
            <div class="gallery__slide gallery__slide--active">
                <img class="gallery__image" src="{{ '/images/gallery/Campus-1.jpg' | relative_url }}" alt="校园正门" loading="lazy">
            </div>
            <div class="gallery__slide">
                <img class="gallery__image" src="{{ '/images/gallery/Campus-2.jpg' | relative_url }}" alt="图书馆大楼" loading="lazy">
            </div>
            <div class="gallery__slide">
                <img class="gallery__image" src="{{ '/images/gallery/Campus-3.jpg' | relative_url }}" alt="教学楼" loading="lazy">
            </div>
            <div class="gallery__slide">
                <img class="gallery__image" src="{{ '/images/gallery/Campus-4.jpg' | relative_url }}" alt="实验中心" loading="lazy">
            </div>
            <div class="gallery__slide">
                <img class="gallery__image" src="{{ '/images/gallery/Campus-5.jpg' | relative_url }}" alt="学生活动中心" loading="lazy">
            </div>
        </div>
        
        <button class="gallery__nav gallery__nav--prev" aria-label="上一张图片">
            <i class="fas fa-chevron-left"></i>
        </button>
        <button class="gallery__nav gallery__nav--next" aria-label="下一张图片">
            <i class="fas fa-chevron-right"></i>
        </button>
        
        <div class="gallery__caption">
            <h3 class="gallery__title">校园正门</h3>
            <p class="gallery__description">学校正门入口，庄严大气，绿树成荫，是学校的标志性建筑之一。</p>
        </div>
        
        <!-- 缩略图导航 -->
        <div class="gallery__thumbnails">
            <button class="gallery__thumb active" data-index="0" aria-label="查看图片1: 校园正门">
                <img src="{{ '/images/gallery/Campus-1.jpg' | relative_url }}" alt="校园正门缩略图" loading="lazy">
            </button>
            <button class="gallery__thumb" data-index="1" aria-label="查看图片2: 图书馆大楼">
                <img src="{{ '/images/gallery/Campus-2.jpg' | relative_url }}" alt="图书馆大楼缩略图" loading="lazy">
            </button>
            <button class="gallery__thumb" data-index="2" aria-label="查看图片3: 教学楼">
                <img src="{{ '/images/gallery/Campus-3.jpg' | relative_url }}" alt="教学楼缩略图" loading="lazy">
            </button>
            <button class="gallery__thumb" data-index="3" aria-label="查看图片4: 实验中心">
                <img src="{{ '/images/gallery/Campus-4.jpg' | relative_url }}" alt="实验中心缩略图" loading="lazy">
            </button>
            <button class="gallery__thumb" data-index="4" aria-label="查看图片5: 学生活动中心">
                <img src="{{ '/images/gallery/Campus-5.jpg' | relative_url }}" alt="学生活动中心缩略图" loading="lazy">
            </button>
        </div>
    </div>
</div>

<style>
/* 画廊基础样式 */
.gallery {
    width: 100%;
    max-width: 900px;
    margin: 2rem auto;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.gallery__container {
    position: relative;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
    background: #f8f9fa;
}

.gallery__slides {
    position: relative;
    aspect-ratio: 16/9;
    width: 100%;
    background: #f0f0f0;
}

.gallery__slide {
    position: absolute;
    inset: 0;
    opacity: 0;
    transition: opacity 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    pointer-events: none;
}

.gallery__slide--active {
    opacity: 1;
    pointer-events: auto;
}

.gallery__image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
}

/* 添加加载状态样式 */
.gallery__image:not([src]) {
    visibility: hidden;
}

.gallery__image.loading {
    opacity: 0.5;
}

/* 导航按钮 */
.gallery__nav {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(255, 255, 255, 0.95);
    border: none;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.2rem;
    color: #2c5282;
    cursor: pointer;
    transition: all 0.2s ease;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
    z-index: 10;
    opacity: 0;
}

.gallery:hover .gallery__nav {
    opacity: 1;
}

.gallery__nav:hover {
    background: #2c5282;
    color: white;
    transform: translateY(-50%) scale(1.1);
    box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}

.gallery__nav--prev {
    left: 20px;
}

.gallery__nav--next {
    right: 20px;
}

/* 图片说明 */
.gallery__caption {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: linear-gradient(transparent, rgba(0, 0, 0, 0.9));
    color: white;
    padding: 1.5rem;
    text-align: center;
    transition: transform 0.3s ease;
    z-index: 5;
}

.gallery__title {
    font-size: 1.4rem;
    margin: 0 0 0.5rem;
    font-weight: 600;
    line-height: 1.3;
}

.gallery__description {
    font-size: 0.95rem;
    margin: 0;
    opacity: 0.9;
    line-height: 1.5;
    max-width: 700px;
    margin: 0 auto;
}

/* 缩略图样式 */
.gallery__thumbnails {
    display: flex;
    justify-content: center;
    gap: 10px;
    padding: 20px;
    background: #f8f9fa;
    border-top: 1px solid #eaeaea;
}

.gallery__thumb {
    width: 80px;
    height: 60px;
    border: none;
    border-radius: 6px;
    overflow: hidden;
    cursor: pointer;
    padding: 0;
    background: transparent;
    transition: all 0.2s ease;
    opacity: 0.6;
}

.gallery__thumb:hover {
    opacity: 0.8;
    transform: translateY(-2px);
}

.gallery__thumb.active {
    opacity: 1;
    border: 3px solid #2c5282;
    box-shadow: 0 4px 8px rgba(44, 82, 130, 0.3);
}

.gallery__thumb img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
}

/* 响应式设计 */
@media (max-width: 768px) {
    .gallery {
        margin: 1rem auto;
        max-width: 95%;
    }
    
    .gallery__nav {
        width: 44px;
        height: 44px;
        font-size: 1rem;
        opacity: 1;
    }
    
    .gallery__nav--prev {
        left: 12px;
    }
    
    .gallery__nav--next {
        right: 12px;
    }
    
    .gallery__title {
        font-size: 1.2rem;
    }
    
    .gallery__description {
        font-size: 0.9rem;
        padding: 0 0.5rem;
    }
    
    .gallery__thumbnails {
        padding: 15px 10px;
        gap: 8px;
    }
    
    .gallery__thumb {
        width: 60px;
        height: 45px;
    }
}

@media (max-width: 480px) {
    .gallery__slides {
        aspect-ratio: 4/3;
    }
    
    .gallery__nav {
        width: 40px;
        height: 40px;
    }
    
    .gallery__caption {
        padding: 1rem;
    }
    
    .gallery__title {
        font-size: 1.1rem;
        margin-bottom: 0.3rem;
    }
    
    .gallery__description {
        font-size: 0.85rem;
    }
    
    .gallery__thumbnails {
        padding: 12px 8px;
        gap: 6px;
    }
    
    .gallery__thumb {
        width: 50px;
        height: 38px;
    }
}

/* 无障碍支持 */
.gallery__nav:focus-visible,
.gallery__thumb:focus-visible {
    outline: 3px solid #4299e1;
    outline-offset: 2px;
}

.gallery__nav:active,
.gallery__thumb:active {
    transform: translateY(-50%) scale(0.95);
}

.gallery__thumb:active {
    transform: translateY(-1px) scale(0.95);
}

/* 深色模式支持 */
@media (prefers-color-scheme: dark) {
    .gallery__container {
        background: #1a202c;
    }
    
    .gallery__nav {
        background: rgba(45, 55, 72, 0.95);
        color: #a0aec0;
    }
    
    .gallery__nav:hover {
        background: #2c5282;
        color: white;
    }
    
    .gallery__caption {
        background: linear-gradient(transparent, rgba(0, 0, 0, 0.95));
    }
    
    .gallery__thumbnails {
        background: #1a202c;
        border-top: 1px solid #2d3748;
    }
    
    .gallery__thumb.active {
        border-color: #4299e1;
        box-shadow: 0 4px 8px rgba(66, 153, 225, 0.3);
    }
}

/* 加载动画 */
@keyframes shimmer {
    0% { background-position: -1000px 0; }
    100% { background-position: 1000px 0; }
}

.gallery__slide--loading::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
    background-size: 1000px 100%;
    animation: shimmer 2s infinite linear;
}
</style>

<script>
class ImageGallery {
    constructor() {
        this.container = document.querySelector('.gallery__container');
        this.slides = document.querySelectorAll('.gallery__slide');
        this.prevBtn = document.querySelector('.gallery__nav--prev');
        this.nextBtn = document.querySelector('.gallery__nav--next');
        this.captionTitle = document.querySelector('.gallery__title');
        this.captionDesc = document.querySelector('.gallery__description');
        this.thumbnails = document.querySelectorAll('.gallery__thumb');
        
        this.currentIndex = 0;
        this.autoSlideInterval = null;
        this.touchStartX = 0;
        this.touchEndX = 0;
        this.isTransitioning = false;
        
        // 图片标题数据
        this.imageData = [
            {
                title: "校园正门",
                description: "学校正门入口，庄严大气，绿树成荫，是学校的标志性建筑之一。"
            },
            {
                title: "图书馆大楼",
                description: "现代化图书馆，藏书丰富，是学生们学习研究的重要场所。"
            },
            {
                title: "教学楼",
                description: "现代化的教学楼，设施齐全，为师生提供了优良的教学环境。"
            },
            {
                title: "实验中心",
                description: "先进的实验中心，配备各类实验设备，支持学生进行科学研究和实践。"
            },
            {
                title: "学生活动中心",
                description: "学生活动中心，各类社团活动、文艺演出和学术讲座在这里举行。"
            }
        ];
        
        this.init();
    }
    
    init() {
        // 检查图片是否正常加载
        this.checkImages();
        
        this.setupEventListeners();
        this.startAutoSlide();
        this.updateCaption();
        this.updateThumbnails();
        
        // 预加载下一张图片
        this.preloadImages();
    }
    
    checkImages() {
        this.slides.forEach((slide, index) => {
            const img = slide.querySelector('img');
            if (img) {
                img.onerror = () => {
                    console.warn(`图片加载失败: ${img.src}`);
                    // 显示备用文本或占位符
                    slide.innerHTML = `
                        <div style="
                            width: 100%; 
                            height: 100%; 
                            display: flex; 
                            flex-direction: column; 
                            align-items: center; 
                            justify-content: center; 
                            background: #f0f0f0; 
                            color: #666;
                        ">
                            <i class="fas fa-image" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                            <p>${this.imageData[index].title}</p>
                            <p style="font-size: 0.9rem;">图片加载中...</p>
                        </div>`;
                };
                
                img.onload = () => {
                    slide.classList.remove('gallery__slide--loading');
                };
            }
        });
    }
    
    setupEventListeners() {
        this.prevBtn.addEventListener('click', () => this.prevSlide());
        this.nextBtn.addEventListener('click', () => this.nextSlide());
        
        // 缩略图点击事件
        this.thumbnails.forEach(thumb => {
            thumb.addEventListener('click', (e) => {
                const index = parseInt(e.currentTarget.dataset.index);
                if (!isNaN(index) && index !== this.currentIndex) {
                    this.goToSlide(index);
                }
            });
        });
        
        // 键盘导航
        document.addEventListener('keydown', (e) => this.handleKeyDown(e));
        
        // 触摸滑动
        this.container.addEventListener('touchstart', (e) => {
            this.touchStartX = e.changedTouches[0].clientX;
        });
        
        this.container.addEventListener('touchend', (e) => {
            this.touchEndX = e.changedTouches[0].clientX;
            this.handleSwipe();
        });
        
        // 鼠标悬停控制自动轮播
        this.container.addEventListener('mouseenter', () => this.stopAutoSlide());
        this.container.addEventListener('mouseleave', () => this.startAutoSlide());
        
        // 焦点管理
        this.container.addEventListener('focusin', () => this.stopAutoSlide());
        this.container.addEventListener('focusout', () => this.startAutoSlide());
    }
    
    prevSlide() {
        if (this.isTransitioning) return;
        this.goToSlide((this.currentIndex - 1 + this.slides.length) % this.slides.length);
    }
    
    nextSlide() {
        if (this.isTransitioning) return;
        this.goToSlide((this.currentIndex + 1) % this.slides.length);
    }
    
    goToSlide(index) {
        if (this.isTransitioning || index === this.currentIndex) return;
        
        this.isTransitioning = true;
        this.currentIndex = index;
        
        // 添加过渡效果
        this.slides.forEach((slide, i) => {
            slide.style.transition = 'opacity 0.4s ease';
            slide.classList.toggle('gallery__slide--active', i === this.currentIndex);
        });
        
        // 更新标题和缩略图
        this.updateCaption();
        this.updateThumbnails();
        
        // 预加载下一张
        const nextIndex = (this.currentIndex + 1) % this.slides.length;
        this.preloadImage(nextIndex);
        
        // 重置过渡状态
        setTimeout(() => {
            this.isTransitioning = false;
            this.slides.forEach(slide => {
                slide.style.transition = '';
            });
        }, 400);
    }
    
    updateSlide() {
        // 更新幻灯片
        this.slides.forEach((slide, index) => {
            slide.classList.toggle('gallery__slide--active', index === this.currentIndex);
        });
        
        // 更新标题
        this.updateCaption();
        
        // 更新缩略图
        this.updateThumbnails();
        
        // 更新ARIA标签
        this.updateAriaLabels();
    }
    
    updateCaption() {
        if (this.currentIndex < this.imageData.length) {
            const data = this.imageData[this.currentIndex];
            this.captionTitle.textContent = data.title;
            this.captionDesc.textContent = data.description;
        }
    }
    
    updateThumbnails() {
        this.thumbnails.forEach((thumb, index) => {
            thumb.classList.toggle('active', index === this.currentIndex);
        });
    }
    
    updateAriaLabels() {
        this.slides.forEach((slide, index) => {
            slide.setAttribute('aria-hidden', index !== this.currentIndex);
            slide.setAttribute('aria-label', `图片 ${index + 1}，共 ${this.slides.length} 张`);
        });
        
        // 更新缩略图ARIA标签
        this.thumbnails.forEach((thumb, index) => {
            const title = this.imageData[index]?.title || `图片 ${index + 1}`;
            thumb.setAttribute('aria-label', `查看${title}，当前${index === this.currentIndex ? '已选中' : '未选中'}`);
        });
    }
    
    handleKeyDown(e) {
        if (e.target.tagName === 'BUTTON' || e.target.tagName === 'I') return;
        
        switch(e.key) {
            case 'ArrowLeft':
                e.preventDefault();
                this.prevSlide();
                break;
            case 'ArrowRight':
                e.preventDefault();
                this.nextSlide();
                break;
            case 'Home':
                e.preventDefault();
                this.goToSlide(0);
                break;
            case 'End':
                e.preventDefault();
                this.goToSlide(this.slides.length - 1);
                break;
            case ' ':
            case 'Spacebar':
                e.preventDefault();
                this.stopAutoSlide();
                setTimeout(() => this.startAutoSlide(), 3000);
                break;
        }
    }
    
    handleSwipe() {
        if (this.isTransitioning) return;
        
        const SWIPE_THRESHOLD = 50;
        const diff = this.touchStartX - this.touchEndX;
        
        if (Math.abs(diff) > SWIPE_THRESHOLD) {
            if (diff > 0) {
                this.nextSlide();
            } else {
                this.prevSlide();
            }
        }
    }
    
    preloadImages() {
        // 预加载所有图片
        for (let i = 1; i < this.slides.length; i++) {
            this.preloadImage(i);
        }
    }
    
    preloadImage(index) {
        const slide = this.slides[index];
        const img = slide.querySelector('img');
        if (img && img.src) {
            const preloadImg = new Image();
            preloadImg.src = img.src;
        }
    }
    
    startAutoSlide() {
        if (this.autoSlideInterval) return;
        this.autoSlideInterval = setInterval(() => this.nextSlide(), 5000);
    }
    
    stopAutoSlide() {
        if (this.autoSlideInterval) {
            clearInterval(this.autoSlideInterval);
            this.autoSlideInterval = null;
        }
    }
}

// 初始化画廊
document.addEventListener('DOMContentLoaded', () => {
    new ImageGallery();
});
</script>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" crossorigin="anonymous" referrerpolicy="no-referrer">
