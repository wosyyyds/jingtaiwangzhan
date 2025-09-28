<template>
    <div class="about">
        <section class="hero-section">
            <div class="hero-overlay"></div>
            <div class="hero-content">
                <h1>关于<span>我们</span></h1>
                <p class="subtitle">探索我们的故事与使命</p>
            </div>
        </section>

        <div class="container">
            <div class="about-content">
                <div class="about-text">
                    <h2>我们的<span>故事</span></h2>
                    <p>这是一个使用Vue.js构建的静态网站示例，旨在展示现代前端技术的应用。我们致力于通过简洁优雅的设计和高效的代码，为用户提供流畅的浏览体验。</p>
                    <p>这个项目最初是为了测试网站部署流程而创建，但现在已经发展成为一个展示前端开发最佳实践的示例平台。</p>
                    
                    <div class="stats-container">
                        <div class="stat-item">
                            <div class="stat-number" data-count="3">0</div>
                            <div class="stat-label">技术栈</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number" data-count="2023">0</div>
                            <div class="stat-label">创立年份</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number" data-count="99">0</div>
                            <div class="stat-label">满意度</div>
                        </div>
                    </div>
                </div>

                <div class="about-image">
                    <img src="https://images.unsplash.com/photo-1555066931-4365d14bab8c?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80" alt="关于我们" class="img-fluid">
                    <div class="image-overlay"></div>
                </div>
            </div>

            <div class="mission-section">
                <h2>我们的<span>使命</span></h2>
                <p>我们致力于通过技术创新和卓越设计，为用户提供最佳的网页浏览体验。我们的目标是：</p>
                <ul class="mission-list">
                    <li>
                        <div class="mission-icon">🚀</div>
                        <div class="mission-text">推动前端技术发展</div>
                    </li>
                    <li>
                        <div class="mission-icon">🎨</div>
                        <div class="mission-text">创造视觉美感</div>
                    </li>
                    <li>
                        <div class="mission-icon">⚡</div>
                        <div class="mission-text">优化性能体验</div>
                    </li>
                    <li>
                        <div class="mission-icon">🌐</div>
                        <div class="mission-text">构建响应式设计</div>
                    </li>
                </ul>
            </div>

            <div class="team-section">
                <h2>我们的<span>团队</span></h2>
                <div class="team-members">
                    <div class="member-card">
                        <div class="member-avatar">
                            <img src="https://randomuser.me/api/portraits/women/44.jpg" alt="团队成员">
                        </div>
                        <h3>张设计师</h3>
                        <p>UI/UX设计师</p>
                        <div class="social-links">
                            <a href="#"><i class="fab fa-twitter"></i></a>
                            <a href="#"><i class="fab fa-linkedin"></i></a>
                            <a href="#"><i class="fab fa-github"></i></a>
                        </div>
                    </div>
                    <div class="member-card">
                        <div class="member-avatar">
                            <img src="https://randomuser.me/api/portraits/men/32.jpg" alt="团队成员">
                        </div>
                        <h3>李开发</h3>
                        <p>前端工程师</p>
                        <div class="social-links">
                            <a href="#"><i class="fab fa-twitter"></i></a>
                            <a href="#"><i class="fab fa-linkedin"></i></a>
                            <a href="#"><i class="fab fa-github"></i></a>
                        </div>
                    </div>
                    <div class="member-card">
                        <div class="member-avatar">
                            <img src="https://randomuser.me/api/portraits/women/68.jpg" alt="团队成员">
                        </div>
                        <h3>王测试</h3>
                        <p>质量保证</p>
                        <div class="social-links">
                            <a href="#"><i class="fab fa-twitter"></i></a>
                            <a href="#"><i class="fab fa-linkedin"></i></a>
                            <a href="#"><i class="fab fa-github"></i></a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { onMounted } from 'vue';

onMounted(() => {
    // 数字动画效果
    const statNumbers = document.querySelectorAll('.stat-number');
    const options = {
        threshold: 0.5
    };

    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                const target = entry.target;
                const count = parseInt(target.getAttribute('data-count'));
                const duration = 2000; // 动画持续时间
                const step = Math.floor(duration / count);
                let current = 0;
                
                const timer = setInterval(() => {
                    current += 1;
                    target.textContent = current;
                    if (current >= count) {
                        clearInterval(timer);
                    }
                }, step);
                
                observer.unobserve(target);
            }
        });
    }, options);

    statNumbers.forEach(number => {
        observer.observe(number);
    });
});
</script>

<style scoped>
.about {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: #2c3e50;
}

.hero-section {
    position: relative;
    height: 400px;
    background: url('https://images.unsplash.com/photo-1499750310107-5fef28a66643?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80') no-repeat center center;
    background-size: cover;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    margin-bottom: 60px;
}

.hero-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
}

.hero-content {
    position: relative;
    z-index: 1;
    color: white;
    padding: 0 20px;
}

.hero-content h1 {
    font-size: 3.5rem;
    margin-bottom: 1rem;
    font-weight: 700;
}

.hero-content h1 span {
    color: #6e8efb;
}

.subtitle {
    font-size: 1.5rem;
    opacity: 0.9;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

.about-content {
    display: flex;
    gap: 40px;
    margin-bottom: 80px;
    align-items: center;
}

.about-text {
    flex: 1;
}

.about-text h2 {
    font-size: 2.5rem;
    margin-bottom: 1.5rem;
    font-weight: 700;
}

.about-text h2 span {
    color: #6e8efb;
}

.about-text p {
    line-height: 1.8;
    margin-bottom: 1.5rem;
    color: #34495e;
    font-size: 1.1rem;
}

.about-image {
    flex: 1;
    position: relative;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.about-image img {
    width: 100%;
    height: auto;
    display: block;
}

.image-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(135deg, rgba(110, 142, 251, 0.3), rgba(167, 119, 227, 0.3));
}

.stats-container {
    display: flex;
    justify-content: space-between;
    margin-top: 40px;
}

.stat-item {
    text-align: center;
    flex: 1;
}

.stat-number {
    font-size: 3rem;
    font-weight: 700;
    color: #6e8efb;
    margin-bottom: 10px;
}

.stat-label {
    font-size: 1.1rem;
    color: #7f8c8d;
}

.mission-section {
    margin-bottom: 80px;
}

.mission-section h2 {
    font-size: 2.5rem;
    margin-bottom: 1.5rem;
    font-weight: 700;
    text-align: center;
}

.mission-section h2 span {
    color: #6e8efb;
}

.mission-section p {
    text-align: center;
    max-width: 700px;
    margin: 0 auto 40px;
    line-height: 1.8;
    color: #34495e;
    font-size: 1.1rem;
}

.mission-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 30px;
    list-style: none;
    padding: 0;
}

.mission-list li {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
    text-align: center;
    transition: all 0.3s ease;
}

.mission-list li:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}

.mission-icon {
    font-size: 2.5rem;
    margin-bottom: 15px;
}

.mission-text {
    font-size: 1.2rem;
    font-weight: 600;
}

.team-section {
    margin-bottom: 80px;
}

.team-section h2 {
    font-size: 2.5rem;
    margin-bottom: 1.5rem;
    font-weight: 700;
    text-align: center;
}

.team-section h2 span {
    color: #6e8efb;
}

.team-members {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 30px;
    margin-top: 40px;
}

.member-card {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
    text-align: center;
    transition: all 0.3s ease;
}

.member-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}

.member-avatar {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    overflow: hidden;
    margin: 0 auto 20px;
    border: 5px solid #f1f1f1;
}

.member-avatar img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.member-card h3 {
    font-size: 1.5rem;
    margin-bottom: 5px;
    color: #2c3e50;
}

.member-card p {
    color: #7f8c8d;
    margin-bottom: 15px;
}

.social-links {
    display: flex;
    justify-content: center;
    gap: 15px;
}

.social-links a {
    color: #6e8efb;
    font-size: 1.2rem;
    transition: all 0.3s ease;
}

.social-links a:hover {
    color: #a777e3;
    transform: translateY(-2px);
}

@media (max-width: 768px) {
    .hero-content h1 {
        font-size: 2.5rem;
    }
    
    .about-content {
        flex-direction: column;
    }
    
    .about-text, .about-image {
        width: 100%;
    }
    
    .mission-list {
        grid-template-columns: 1fr 1fr;
    }
    
    .team-members {
        grid-template-columns: 1fr;
    }
}

@media (max-width: 480px) {
    .hero-section {
        height: 300px;
    }
    
    .hero-content h1 {
        font-size: 2rem;
    }
    
    .subtitle {
        font-size: 1.2rem;
    }
    
    .stats-container {
        flex-direction: column;
        gap: 20px;
    }
    
    .mission-list {
        grid-template-columns: 1fr;
    }
}
</style>