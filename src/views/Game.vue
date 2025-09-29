<template>
  <div class="games-container">
    <!-- 英雄区域 -->
    <div class="hero-section">
      <div class="hero-overlay"></div>
      <div class="hero-content">
        <h1>🎮 游戏中心</h1>
        <p class="subtitle">探索精彩游戏世界，享受无限乐趣</p>
        <div class="search-bar">
          <input type="text" placeholder="搜索游戏..." v-model="searchQuery">
          <button class="search-btn">🔍</button>
        </div>
      </div>
    </div>

    <!-- 游戏分类导航 -->
    <div class="categories">
      <button 
        v-for="category in categories" 
        :key="category" 
        :class="['category-btn', activeCategory === category ? 'active' : '']"
        @click="setActiveCategory(category)"
      >
        {{ category }}
      </button>
    </div>

    <!-- 游戏网格 -->
    <div class="games-grid">
      <div 
        class="game-card" 
        v-for="game in filteredGames" 
        :key="game.id" 
        @click="playGame(game)"
        :style="{ 'background-image': `linear-gradient(rgba(0,0,0,0.3), rgba(0,0,0,0.3)), url('${getGameBg(game.id)}')` }"
      >
        <div class="game-icon">{{ game.icon }}</div>
        <h3>{{ game.name }}</h3>
        <p>{{ game.description }}</p>
        <div class="game-tags">
          <span class="tag">{{ game.category }}</span>
          <span class="tag">{{ game.difficulty }}</span>
        </div>
        <div class="game-rating">
          <span v-for="star in 5" :key="star" :class="['star', star <= game.rating ? 'filled' : '']">★</span>
        </div>
      </div>
    </div>

    <!-- 精选游戏轮播 -->
    <div class="featured-games">
      <h2>🔥 精选推荐</h2>
      <div class="carousel">
        <div 
          class="featured-game" 
          v-for="(game, index) in featuredGames" 
          :key="index"
          @click="playGame(game)"
          :style="{ 'background-image': `linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), url('${getGameBg(game.id)}')` }"
        >
          <div class="featured-content">
            <h3>{{ game.name }}</h3>
            <p>{{ game.description }}</p>
            <button class="play-btn">立即游玩</button>
          </div>
        </div>
      </div>
    </div>

    <!-- 使用说明 -->
    <div class="instructions">
      <h2>📌 使用说明</h2>
      <div class="instruction-cards">
        <div class="instruction-card">
          <div class="instruction-icon">🖱️</div>
          <h3>操作简单</h3>
          <p>点击游戏卡片即可开始游戏</p>
        </div>
        <div class="instruction-card">
          <div class="instruction-icon">⌨️</div>
          <h3>键盘控制</h3>
          <p>使用键盘方向键或WASD控制游戏</p>
        </div>
        <div class="instruction-card">
          <div class="instruction-icon">🎯</div>
          <h3>高分挑战</h3>
          <p>挑战自我，创造高分记录</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// 搜索查询
const searchQuery = ref('')
// 活动分类
const activeCategory = ref('全部')

// 游戏分类
const categories = ref(['全部', '休闲', '益智', '动作', '策略', '射击'])

// 游戏列表数据
const games = ref([
  {
    id: 'snake',
    name: '贪吃蛇',
    icon: '🐍',
    description: '经典的贪吃蛇游戏，控制蛇吃食物并避免撞墙',
    category: '休闲',
    difficulty: '简单',
    path: '/html_files/游戏.html',
    rating: 4
  },
  {
    id: 'breakout',
    name: '打砖块',
    icon: '🧱',
    description: '控制挡板反弹球击碎砖块',
    category: '动作',
    difficulty: '中等',
    path: '/html_files/打砖块.html',
    rating: 5
  },
  {
    id: '2048',
    name: '2048',
    icon: '🔢',
    description: '滑动方块合并数字，目标是合成2048',
    category: '益智',
    difficulty: '困难',
    path: '/html_files/2048.html',
    rating: 4
  },
  {
    id: 'tetris',
    name: '俄罗斯方块',
    icon: '🔳',
    description: '经典俄罗斯方块游戏，消除完整行获得分数',
    category: '益智',
    difficulty: '中等',
    path: '/html_files/俄罗斯方块.html',
    rating: 5
  },
  {
    id: 'snake-enhanced',
    name: '贪食蛇增强版',
    icon: '🐍',
    description: '增强版贪食蛇游戏，包含多种特殊食物和道具',
    category: '休闲',
    difficulty: '困难',
    path: '/html_files/贪食蛇增强版.html',
    rating: 3
  },
  {
    id: 'minesweeper',
    name: '扫雷',
    icon: '💣',
    description: '经典扫雷游戏，根据数字提示避开地雷',
    category: '益智',
    difficulty: '中等',
    path: '/html_files/扫雷.html',
    rating: 4
  },
  {
    id: 'othello',
    name: '黑白棋',
    icon: '⚫⚪',
    description: '经典的黑白棋游戏，策略性极强',
    category: '策略',
    difficulty: '困难',
    path: '/html_files/黑白棋.html',
    rating: 4
  },
  {
    id: 'catch-ball',
    name: '接球游戏',
    icon: '⚽',
    description: '控制挡板接住下落的各种球类获得分数',
    category: '动作',
    difficulty: '中等',
    path: '/html_files/接球游戏.html',
    rating: 3
  },
  {
    id: 'Space',
    name: '太空射击',
    icon: '🚀',
    description: '控制飞船射击外星人，同时躲避敌人的攻击',
    category: '射击',
    difficulty: '中等',
    path: '/html_files/太空射击.html',
    rating: 5
  },
  {
    id: 'push-the-box',
    name: '推箱子',
    icon: '📦',
    description: '将所有箱子推到目标位置',
    category: '休闲',
    difficulty: '中等',
    path: '/html_files/推箱子.html',
    rating: 3
  },
  {
    id: 'huarongdao',
    name: '华容道',
    icon: '🎯',
    description: '滑动方块帮助曹操逃脱',
    category: '益智',
    difficulty: '困难',
    path: '/html_files/华容道.html',
    rating: 4
  },
  {
    id: 'puzzle',
    name: '拼图',
    icon: '🧩',
    description: '完成图片拼图挑战',
    category: '益智',
    difficulty: '简单',
    path: '/html_files/拼图.html',
    rating: 3
  },
  {
    id: 'pingpong',
    name: '双人乒乓球',
    icon: '🏓',
    description: '本地双人对战，控制球拍互相对打，反应与走位的较量',
    category: '益智',
    difficulty: '简单',
    path: '/html_files/双人乒乓球.html',
    rating: 3
  },
  {
    id: 'tictactoe',
    name: '双人井字棋',
    icon: '⭕✖️',
    description: '经典二人回合制游戏，轮流落子，先连成三子的一方获胜',
    category: '益智',
    difficulty: '简单',
    path: '/html_files/双人井字棋.html',
    rating: 3
  },
  {
    id: 'snake-dual',
    name: '双人贪吃蛇',
    icon: '🐍👥',
    description: '本地双人对战：两名玩家同时操作各自的蛇，抢夺食物并躲避碰撞，考验反应与策略',
    category: '益智',
    difficulty: '简单',
    path: '/html_files/双人贪吃蛇.html',
    rating: 3
  },
  {
    id: 'tetris-dual',
    name: '双人俄罗斯方块',
    icon: '🔳🔳',
    description: '双人对战俄罗斯方块：互相发送障碍，争夺更高分数与生存时间，适合竞速与策略型玩家',
    category: '益智',
    difficulty: '简单',
    path: '/html_files/双人俄罗斯方块.html',
    rating: 3
  }
])

// 精选游戏
const featuredGames = computed(() => {
  return [...games.value].sort((a, b) => b.rating - a.rating).slice(0, 3)
})

// 过滤后的游戏
const filteredGames = computed(() => {
  let filtered = games.value
  
  // 按分类过滤
  if (activeCategory.value !== '全部') {
    filtered = filtered.filter(game => game.category === activeCategory.value)
  }
  
  // 按搜索查询过滤
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    filtered = filtered.filter(game => 
      game.name.toLowerCase().includes(query) || 
      game.description.toLowerCase().includes(query)
    )
  }
  
  return filtered
})

// 设置活动分类
const setActiveCategory = (category) => {
  activeCategory.value = category
}

// 获取游戏背景图
const getGameBg = (id) => {
  const gameBgs = {
    snake: 'https://images.unsplash.com/photo-1597334948330-1d7ef3a1a6c1?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    breakout: 'https://images.unsplash.com/photo-1542751371-adc38448a05e?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    '2048': 'https://images.unsplash.com/photo-1518770660439-4636190af475?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    tetris: 'https://images.unsplash.com/photo-1560253023-3ec5d502959f?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    'snake-enhanced': 'https://images.unsplash.com/photo-1597334948330-1d7ef3a1a6c1?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    minesweeper: 'https://images.unsplash.com/photo-1563089145-599997674d42?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    othello: 'https://images.unsplash.com/photo-1589998059171-988d887df646?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    'catch-ball': 'https://images.unsplash.com/photo-1574629810360-7efbbe195018?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    Space: 'https://images.unsplash.com/photo-1451187580459-43490279c0fa?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    'push-the-box': 'https://images.unsplash.com/photo-1579783902614-a3fb39268b59?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    huarongdao: 'https://images.unsplash.com/photo-1589998059171-988d887df646?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    puzzle: 'https://images.unsplash.com/photo-1605106702734-205df224ecce?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80'
  ,
  pingpong: 'https://images.unsplash.com/photo-1509223197845-458d87318791?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
  tictactoe: 'https://images.unsplash.com/photo-1545239351-1141bd82e8a6?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80'
  ,
  'snake-dual': 'https://images.unsplash.com/photo-1505686994434-e3cc1d1d7f82?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
  'tetris-dual': 'https://images.unsplash.com/photo-1602526436134-8b1d95a8f3a6?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80'
  }
  return gameBgs[id] || 'https://images.unsplash.com/photo-1493711662062-fa541adb3fc8?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80'
}

const playGame = (game) => {
  // 使用完整的URL打开游戏页面
  const fullPath = `${window.location.origin}${game.path}`
  window.open(fullPath, '_blank')
}
</script>

<style scoped>
.games-container {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: white;
  max-width: 1400px;
  margin: 0 auto;
}

/* 英雄区域 */
.hero-section {
  position: relative;
  height: 400px;
  background: url('https://images.unsplash.com/photo-1493711662062-fa541adb3fc8?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80') no-repeat center center;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  margin-bottom: 40px;
  border-radius: 15px;
  overflow: hidden;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(110, 142, 251, 0.7), rgba(167, 119, 227, 0.7));
}

.hero-content {
  position: relative;
  z-index: 1;
  padding: 0 20px;
  width: 100%;
  max-width: 800px;
}

.hero-content h1 {
  font-size: 3.5rem;
  margin-bottom: 1rem;
  font-weight: 700;
  text-shadow: 0 2px 4px rgba(0,0,0,0.3);
}

.subtitle {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  opacity: 0.9;
  text-shadow: 0 2px 4px rgba(0,0,0,0.3);
}

.search-bar {
  display: flex;
  max-width: 500px;
  margin: 0 auto;
}

.search-bar input {
  flex: 1;
  padding: 15px 20px;
  border: none;
  border-radius: 50px 0 0 50px;
  font-size: 1rem;
  outline: none;
}

.search-btn {
  padding: 0 25px;
  background: #6e8efb;
  color: white;
  border: none;
  border-radius: 0 50px 50px 0;
  cursor: pointer;
  font-size: 1.2rem;
  transition: all 0.3s ease;
}

.search-btn:hover {
  background: #5a7bf0;
}

/* 分类导航 */
.categories {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-bottom: 40px;
  flex-wrap: wrap;
}

.category-btn {
  padding: 10px 20px;
  background: rgba(255, 255, 255, 0.1);
  color: white;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  font-size: 1rem;
  transition: all 0.3s ease;
  backdrop-filter: blur(5px);
}

.category-btn:hover {
  background: rgba(255, 255, 255, 0.2);
}

.category-btn.active {
  background: #6e8efb;
  font-weight: 600;
}

/* 游戏网格 */
.games-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 30px;
  margin-bottom: 60px;
}

.game-card {
  background-size: cover;
  background-position: center;
  border-radius: 15px;
  padding: 25px;
  cursor: pointer;
  transition: all 0.3s ease;
  text-align: center;
  height: 300px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  position: relative;
  overflow: hidden;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.game-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to top, rgba(0,0,0,0.8) 0%, rgba(0,0,0,0.3) 100%);
}

.game-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
}

.game-icon {
  font-size: 3rem;
  margin-bottom: 15px;
  position: relative;
  z-index: 1;
}

.game-card h3 {
  font-size: 1.5rem;
  margin-bottom: 10px;
  position: relative;
  z-index: 1;
}

.game-card p {
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 20px;
  line-height: 1.5;
  position: relative;
  z-index: 1;
}

.game-tags {
  display: flex;
  justify-content: center;
  gap: 10px;
  position: relative;
  z-index: 1;
}

.tag {
  background: rgba(255, 255, 255, 0.2);
  padding: 5px 15px;
  border-radius: 20px;
  font-size: 0.8rem;
  color: white;
  backdrop-filter: blur(5px);
}

.game-rating {
  margin-top: 15px;
  position: relative;
  z-index: 1;
}

.star {
  color: rgba(255, 255, 255, 0.3);
  font-size: 1.2rem;
}

.star.filled {
  color: #ffcc00;
}

/* 精选游戏轮播 */
.featured-games {
  margin-bottom: 60px;
}

.featured-games h2 {
  font-size: 2rem;
  margin-bottom: 30px;
  color: white;
  text-align: center;
}

.carousel {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
  gap: 30px;
}

.featured-game {
  height: 250px;
  border-radius: 15px;
  background-size: cover;
  background-position: center;
  position: relative;
  overflow: hidden;
  cursor: pointer;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;
}

.featured-game:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
}

.featured-content {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  padding: 30px;
  z-index: 1;
}

.featured-content h3 {
  font-size: 1.8rem;
  margin-bottom: 10px;
}

.featured-content p {
  margin-bottom: 20px;
  color: rgba(255, 255, 255, 0.9);
}

.play-btn {
  padding: 10px 25px;
  background: #6e8efb;
  color: white;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.play-btn:hover {
  background: #5a7bf0;
  transform: translateY(-2px);
}

/* 使用说明 */
.instructions {
  background: rgba(255, 255, 255, 0.1);
  padding: 40px;
  border-radius: 15px;
  margin-bottom: 40px;
  backdrop-filter: blur(5px);
}

.instructions h2 {
  font-size: 2rem;
  margin-bottom: 30px;
  text-align: center;
}

.instruction-cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 30px;
}

.instruction-card {
  background: rgba(255, 255, 255, 0.1);
  padding: 30px;
  border-radius: 15px;
  text-align: center;
  transition: all 0.3s ease;
  backdrop-filter: blur(5px);
}

.instruction-card:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-5px);
}

.instruction-icon {
  font-size: 2.5rem;
  margin-bottom: 20px;
}

.instruction-card h3 {
  font-size: 1.5rem;
  margin-bottom: 15px;
}

.instruction-card p {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .hero-content h1 {
    font-size: 2.5rem;
  }
  
  .subtitle {
    font-size: 1.2rem;
  }
  
  .games-grid, .carousel, .instruction-cards {
    grid-template-columns: 1fr;
  }
  
  .featured-game {
    height: 200px;
  }
  
  .categories {
    gap: 10px;
  }
  
  .category-btn {
    padding: 8px 15px;
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .hero-section {
    height: 350px;
  }
  
  .hero-content h1 {
    font-size: 2rem;
  }
  
  .search-bar input {
    padding: 12px 15px;
  }
  
  .instruction-cards {
    grid-template-columns: 1fr;
  }
}
</style>