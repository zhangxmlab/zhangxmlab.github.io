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
                <img class="gallery__image" src="/images/gallery/Campus-1.jpg" alt="校园正门" loading="lazy">
            </div>
            <div class="gallery__slide">
                <img class="gallery__image" src="/images/gallery/Campus-2.jpg" alt="图书馆大楼" loading="lazy">
            </div>
            <div class="gallery__slide">
                <img class="gallery__image" src="/images/gallery/Campus-3.jpg" alt="教学楼" loading="lazy">
            </div>
            <div class="gallery__slide">
                <img class="gallery__image" src="/images/gallery/Campus-4.jpg" alt="实验中心" loading="lazy">
            </div>
            <div class="gallery__slide">
                <img class="gallery__image" src="/images/gallery/Campus-5.jpg" alt="学生活动中心" loading="lazy">
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
}

/* 无障碍支持 */
.gallery__nav:focus-visible {
    outline: 3px solid #4299e1;
    outline-offset: 2px;
}

.gallery__nav:active {
    transform: translateY(-50%) scale(0.95);
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
        
        this.currentIndex = 0;
        this.autoSlideInterval = null;
        this.touchStartX = 0;
        this.touchEndX = 0;
        
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
        this.setupEventListeners();
        this.startAutoSlide();
        this.updateCaption();
        
        // 预加载下一张图片
        this.preloadImages();
    }
    
    setupEventListeners() {
        this.prevBtn.addEventListener('click', () => this.prevSlide());
        this.nextBtn.addEventListener('click', () => this.nextSlide());
        
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
        this.currentIndex = (this.currentIndex - 1 + this.slides.length) % this.slides.length;
        this.updateSlide();
    }
    
    nextSlide() {
        this.currentIndex = (this.currentIndex + 1) % this.slides.length;
        this.updateSlide();
        
        // 预加载下一张
        const nextIndex = (this.currentIndex + 1) % this.slides.length;
        this.preloadImage(nextIndex);
    }
    
    updateSlide() {
        // 更新幻灯片
        this.slides.forEach((slide, index) => {
            slide.classList.toggle('gallery__slide--active', index === this.currentIndex);
        });
        
        // 更新标题
        this.updateCaption();
        
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
    
    updateAriaLabels() {
        this.slides.forEach((slide, index) => {
            slide.setAttribute('aria-hidden', index !== this.currentIndex);
            slide.setAttribute('aria-label', `图片 ${index + 1}，共 ${this.slides.length} 张`);
        });
    }
    
    handleKeyDown(e) {
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
                this.currentIndex = 0;
                this.updateSlide();
                break;
            case 'End':
                e.preventDefault();
                this.currentIndex = this.slides.length - 1;
                this.updateSlide();
                break;
        }
    }
    
    handleSwipe() {
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
        if (img) {
            const src = img.getAttribute('src');
            if (src) {
                const preloadImg = new Image();
                preloadImg.src = src;
            }
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
