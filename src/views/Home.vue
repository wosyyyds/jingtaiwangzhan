<template>
    <div class="home">
        <header class="hero">
            <h1 class="title">欢迎来到我的静态网站</h1>
            <p class="subtitle">探索创意与技术的完美结合</p>
            <div class="cta-buttons">
                <button class="btn primary">开始探索</button>
                <button class="btn secondary">了解更多</button>
            </div>
        </header>

        <section class="features">
            <div class="feature-card">
                <div class="icon">🚀</div>
                <h3>快速高效</h3>
                <p>基于Vue 3构建，提供流畅的用户体验</p>
            </div>
            <div class="feature-card">
                <div class="icon">🎨</div>
                <h3>精美设计</h3>
                <p>现代化UI设计，响应式布局</p>
            </div>
            <div class="feature-card">
                <div class="icon">🔒</div>
                <h3>安全可靠</h3>
                <p>静态网站，无服务器安全风险</p>
            </div>
        </section>

        <section class="content">
            <h2>这是一个使用Vue创建的静态网站示例</h2>
            <p>这个网站展示了如何使用Vue 3和现代CSS技术创建一个美观、响应式的静态网站。它包含了现代化的设计元素，如卡片布局、微交互和渐变色。</p>
        </section>
    </div>
</template>

<script setup>
// 可以在这里添加交互逻辑
</script>

<style scoped>
.home {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: #2c3e50;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

.hero {
    text-align: center;
    padding: 80px 0;
    background: linear-gradient(135deg, #6e8efb, #a777e3);
    color: white;
    border-radius: 10px;
    margin: 20px 0;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.title {
    font-size: 3rem;
    margin-bottom: 1rem;
    font-weight: 700;
}

.subtitle {
    font-size: 1.5rem;
    opacity: 0.9;
    margin-bottom: 2rem;
}

.cta-buttons {
    display: flex;
    justify-content: center;
    gap: 15px;
}

.btn {
    padding: 12px 24px;
    border: none;
    border-radius: 50px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
}

.btn.primary {
    background-color: white;
    color: #6e8efb;
}

.btn.secondary {
    background-color: transparent;
    color: white;
    border: 2px solid white;
}

.btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.features {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
    margin: 50px 0;
}

.feature-card {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
    transition: all 0.3s ease;
    text-align: center;
}

.feature-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

.feature-card .icon {
    font-size: 3rem;
    margin-bottom: 1rem;
}

.feature-card h3 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    color: #2c3e50;
}

.feature-card p {
    color: #7f8c8d;
    line-height: 1.6;
}

.content {
    background: #f9f9f9;
    padding: 40px;
    border-radius: 10px;
    margin: 40px 0;
}

.content h2 {
    font-size: 2rem;
    margin-bottom: 1rem;
    color: #2c3e50;
}

.content p {
    line-height: 1.8;
    color: #34495e;
}

@media (max-width: 768px) {
    .title {
        font-size: 2.5rem;
    }
    
    .subtitle {
        font-size: 1.2rem;
    }
    
    .features {
        grid-template-columns: 1fr;
    }
    
    .cta-buttons {
        flex-direction: column;
        align-items: center;
    }
}
</style>