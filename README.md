<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>星际电影 - 探索奇幻影视世界</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.8/dist/chart.umd.min.js"></script>
  
  <!-- 配置Tailwind自定义主题 -->
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            primary: '#6C5CE7',      // 主色调：深紫色
            secondary: '#00CEFF',    // 辅助色：霓虹蓝
            accent: '#FF2E63',       // 强调色：霓虹粉
            dark: '#131022',         // 深色背景
            darker: '#0A0814',       // 更深色背景
            light: '#F54',       // 更深色背景
            light: '#F5F5F5',        // 浅色文本
          },
          fontFamily: {
            sans: ['Inter', 'system-ui', 'sans-serif'],
            display: ['Orbitron', 'sans-serif'], // 科幻风格字体
          },
          backgroundImage: {
            'gradient-radial': 'radial-gradient(var(--tw-gradient-stops))',
            'nebula': "url('https://picsum.photos/id/1002/1920/1080')",
          },
          animation: {
            'float': 'float 3s ease-in-out infinite',
            'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
            'glow': 'glow 2s ease-in-out infinite alternate',
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0)' },
              '50%': { transform: 'translateY(-10px)' },
            },
            glow: {
              '0%': { textShadow: '0 0 5px rgba(108, 92, 231, 0.7), 0 0 10px rgba(108, 92, 231, 0.5)' },
              '100%': { textShadow: '0 0 10px rgba(0, 206, 255, 0.7), 0 0 20px rgba(0, 206, 255, 0.5), 0 0 30px rgba(0, 206, 255, 0.3)' },
            }
          },
        },
      }
    }
  </script>
  
  <!-- 自定义工具类 -->
  <style type="text/tailwindcss">
    @layer utilities {
      .content-auto {
        content-visibility: auto;
      }
      .text-shadow {
        text-shadow: 0 0 8px rgba(108, 92, 231, 0.5);
      }
      .text-shadow-glow {
        text-shadow: 0 0 10px rgba(0, 206, 255, 0.7), 0 0 20px rgba(0, 206, 255, 0.5);
      }
      .backdrop-blur-xl {
        backdrop-filter: blur(20px);
      }
      .scrollbar-hidden::-webkit-scrollbar {
        display: none;
      }
      .scrollbar-hidden {
        -ms-overflow-style: none;
        scrollbar-width: none;
      }
      .clip-path-slant {
        clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
      }
    }
  </style>
  
  <!-- 导入科幻风格字体 -->
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;600;700&display=swap" rel="stylesheet">
</head>

<body class="bg-dark text-light font-sans overflow-x-hidden">
  <!-- 背景特效 -->
  <div class="fixed inset-0 z-0 opacity-20">
    <div class="absolute top-0 left-0 w-full h-full bg-gradient-radial from-primary/20 to-transparent"></div>
    <div class="absolute top-0 left-0 w-full h-full" id="stars"></div>
  </div>

  <!-- 导航栏 -->
  <header class="fixed top-0 left-0 w-full z-50 transition-all duration-500" id="navbar">
    <div class="container mx-auto px-4 py-4 flex items-center justify-between backdrop-blur-xl bg-dark/60 border-b border-primary/20">
      <a href="index.html" class="flex items-center space-x-2">
        <div class="w-10 h-10 rounded-full bg-gradient-to-r from-primary to-secondary flex items-center justify-center animate-pulse-slow">
          <i class="fa fa-film text-white text-xl"></i>
        </div>
        <h1 class="text-2xl font-display font-bold text-shadow-glow animate-glow">星际电影</h1>
      </a>
      
      <!-- 桌面导航 -->
      <nav class="hidden md:flex items-center space-x-8">
        <a href="index.html" class="text-white hover:text-secondary transition-colors duration-300 font-medium">首页</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium">分类</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium">排行榜</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium">新上线</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium">关于</a>
      </nav>
      
      <!-- 搜索框 -->
      <div class="relative hidden md:block w-64">
        <input 
          type="text" 
          id="searchInput" 
          placeholder="搜索电影..." 
          class="w-full bg-darker/80 text-white border border-primary/30 rounded-full py-2 pl-10 pr-4 focus:outline-none focus:border-secondary transition-all duration-300"
        >
        <i class="fa fa-search absolute left-3 top-3 text-primary"></i>
      </div>
      
      <!-- 用户菜单 -->
      <div class="hidden md:flex items-center space-x-4">
        <button class="w-10 h-10 rounded-full bg-darker/80 flex items-center justify-center border border-primary/30 hover:border-secondary transition-all duration-300" id="notificationBtn">
          <i class="fa fa-bell-o text-white"></i>
        </button>
        <button class="w-10 h-10 rounded-full bg-darker/80 flex items-center justify-center border border-primary/30 hover:border-secondary transition-all duration-300" id="bookmarkBtn">
          <i class="fa fa-bookmark-o text-white"></i>
        </button>
        <button class="w-10 h-10 rounded-full overflow-hidden border-2 border-secondary" id="userMenuBtn">
          <img src="https://picsum.photos/id/1027/200/200" alt="用户头像" class="w-full h-full object-cover">
        </button>
      </div>
      
      <!-- 移动端菜单按钮 -->
      <button class="md:hidden text-white text-2xl" id="mobileMenuBtn">
        <i class="fa fa-bars"></i>
      </button>
    </div>
    
    <!-- 移动端菜单 -->
    <div class="md:hidden hidden bg-dark/95 backdrop-blur-xl border-b border-primary/20" id="mobileMenu">
      <div class="container mx-auto px-4 py-4 flex flex-col space-y-4">
        <div class="relative">
          <input 
            type="text" 
            placeholder="搜索电影..." 
            class="w-full bg-darker/80 text-white border border-primary/30 rounded-full py-2 pl-10 pr-4 focus:outline-none focus:border-secondary"
          >
          <i class="fa fa-search absolute left-3 top-3 text-primary"></i>
        </div>
        <a href="index.html" class="text-white hover:text-secondary transition-colors duration-300 font-medium py-2">首页</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium py-2">分类</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium py-2">排行榜</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium py-2">新上线</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium py-2">关于</a>
        <div class="flex items-center space-x-4 pt-2">
          <button class="w-10 h-10 rounded-full bg-darker/80 flex items-center justify-center border border-primary/30 hover:border-secondary transition-all duration-300">
            <i class="fa fa-bell-o text-white"></i>
          </button>
          <button class="w-10 h-10 rounded-full bg-darker/80 flex items-center justify-center border border-primary/30 hover:border-secondary transition-all duration-300">
            <i class="fa fa-bookmark-o text-white"></i>
          </button>
          <div class="w-10 h-10 rounded-full overflow-hidden border-2 border-secondary">
            <img src="https://picsum.photos/id/1027/200/200" alt="用户头像" class="w-full h-full object-cover">
          </div>
        </div>
      </div>
    </div>
    
    <!-- 用户下拉菜单 -->
    <div class="hidden absolute top-20 right-4 bg-darker/95 backdrop-blur-xl border border-primary/20 rounded-xl w-64 p-4 shadow-xl z-50" id="userMenu">
      <div class="flex items-center space-x-3 mb-4">
        <div class="w-12 h-12 rounded-full overflow-hidden">
          <img src="https://picsum.photos/id/1027/200/200" alt="用户头像" class="w-full h-full object-cover">
        </div>
        <div>
          <h4 class="font-bold text-white">旅行者1号</h4>
          <p class="text-white/70 text-sm">高级会员</p>
        </div>
      </div>
      
      <div class="space-y-2">
        <a href="#" class="block px-3 py-2 rounded-lg hover:bg-primary/10 transition-colors duration-300 flex items-center">
          <i class="fa fa-user-o mr-2 text-secondary"></i>
          <span>个人资料</span>
        </a>
        <a href="#" class="block px-3 py-2 rounded-lg hover:bg-primary/10 transition-colors duration-300 flex items-center">
          <i class="fa fa-bookmark-o mr-2 text-secondary"></i>
          <span>我的收藏</span>
        </a>
        <a href="#" class="block px-3 py-2 rounded-lg hover:bg-primary/10 transition-colors duration-300 flex items-center">
          <i class="fa fa-history mr-2 text-secondary"></i>
          <span>观看历史</span>
        </a>
        <a href="#" class="block px-3 py-2 rounded-lg hover:bg-primary/10 transition-colors duration-300 flex items-center">
          <i class="fa fa-cog mr-2 text-secondary"></i>
          <span>设置</span>
        </a>
        <div class="border-t border-gray-800 my-2"></div>
        <a href="#" class="block px-3 py-2 rounded-lg hover:bg-primary/10 transition-colors duration-300 flex items-center text-red-400">
          <i class="fa fa-sign-out mr-2"></i>
          <span>退出登录</span>
        </a>
      </div>
    </div>
  </header>

  <!-- 主内容 -->
  <main class="pt-24 pb-16 relative z-10">
    <!-- 英雄区域 -->
    <section class="relative mb-16 overflow-hidden">
      <div class="absolute inset-0 h-[80vh] bg-cover bg-center clip-path-slant" style="background-image: url('https://picsum.photos/id/1019/1920/1080');">
        <div class="absolute inset-0 bg-gradient-to-r from-dark via-dark/70 to-transparent"></div>
      </div>
      
      <div class="container mx-auto px-4 pt-20 pb-16 relative z-10">
        <div class="max-w-2xl">
          <span class="px-3 py-1 bg-accent text-white text-xs font-bold rounded-full">热门推荐</span>
          <h1 class="text-[clamp(2rem,5vw,4rem)] font-display font-bold text-shadow-glow mt-4 mb-6">星际穿越</h1>
          <p class="text-white/80 text-lg mb-8 leading-relaxed">
            当太阳系面临崩溃，一组探险家穿越虫洞，试图为人类寻找新家园。在时间和空间的维度中，他们必须面对人类认知的极限...
          </p>
          <div class="flex flex-wrap gap-4">
            <button class="px-8 py-3 bg-gradient-to-r from-primary to-secondary text-white font-bold rounded-full flex items-center hover:shadow-lg hover:shadow-primary/30 transition-all duration-300 transform hover:-translate-y-1 movie-detail-btn" data-id="1">
              <i class="fa fa-play-circle mr-2"></i> 立即观看
            </button>
            <button class="px-8 py-3 bg-darker/80 border border-white/20 text-white font-bold rounded-full flex items-center hover:border-secondary hover:text-secondary transition-all duration-300">
              <i class="fa fa-plus mr-2"></i> 加入列表
            </button>
            <button class="px-8 py-3 bg-darker/80 border border-white/20 text-white font-bold rounded-full flex items-center hover:border-secondary hover:text-secondary transition-all duration-300">
              <i class="fa fa-share-alt mr-2"></i> 分享
            </button>
          </div>
        </div>
      </div>
      
      <!-- 滚动指示器 -->
      <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 flex flex-col items-center animate-bounce">
        <span class="text-white/70 mb-2 text-sm">向下滚动</span>
        <i class="fa fa-angle-down text-white"></i>
      </div>
    </section>
    
    <!-- 分类导航 -->
    <section class="container mx-auto px-4 mb-12">
      <div class="overflow-x-auto pb-4 scrollbar-hidden">
        <div class="flex space-x-3 min-w-max">
          <button class="px-6 py-2 bg-primary text-white rounded-full whitespace-nowrap">全部</button>
          <button class="px-6 py-2 bg-darker/80 border border-primary/30 rounded-full text-white hover:border-secondary transition-all duration-300 whitespace-nowrap">科幻</button>
          <button class="px-6 py-2 bg-darker/80 border border-primary/30 rounded-full text-white hover:border-secondary transition-all duration-300 whitespace-nowrap">动作</button>
          <button class="px-6 py-2 bg-darker/80 border border-primary/30 rounded-full text-white hover:border-secondary transition-all duration-300 whitespace-nowrap">奇幻</button>
          <button class="px-6 py-2 bg-darker/80 border border-primary/30 rounded-full text-white hover:border-secondary transition-all duration-300 whitespace-nowrap">冒险</button>
          <button class="px-6 py-2 bg-darker/80 border border-primary/30 rounded-full text-white hover:border-secondary transition-all duration-300 whitespace-nowrap">悬疑</button>
          <button class="px-6 py-2 bg-darker/80 border border-primary/30 rounded-full text-white hover:border-secondary transition-all duration-300 whitespace-nowrap">惊悚</button>
          <button class="px-6 py-2 bg-darker/80 border border-primary/30 rounded-full text-white hover:border-secondary transition-all duration-300 whitespace-nowrap">喜剧</button>
          <button class="px-6 py-2 bg-darker/80 border border-primary/30 rounded-full text-white hover:border-secondary transition-all duration-300 whitespace-nowrap">爱情</button>
        </div>
      </div>
    </section>
    
    <!-- 热门电影 -->
    <section class="container mx-auto px-4 mb-16">
      <div class="flex justify-between items-center mb-6">
        <h2 class="text-2xl font-display font-bold text-white">热门电影</h2>
        <div class="flex space-x-2">
          <button class="w-10 h-10 rounded-full bg-darker/80 border border-primary/30 flex items-center justify-center text-white hover:border-secondary transition-all duration-300" id="prevHot">
            <i class="fa fa-angle-left"></i>
          </button>
          <button class="w-10 h-10 rounded-full bg-darker/80 border border-primary/30 flex items-center justify-center text-white hover:border-secondary transition-all duration-300" id="nextHot">
            <i class="fa fa-angle-right"></i>
          </button>
        </div>
      </div>
      
      <div class="relative">
        <div class="overflow-x-auto pb-6 scrollbar-hidden" id="hotMovies">
          <div class="flex space-x-4 min-w-max">
            <!-- 电影卡片1 -->
            <div class="movie-card w-64 flex-shrink-0 group">
              <div class="relative rounded-xl overflow-hidden mb-3">
                <img src="https://picsum.photos/id/1025/300/450" alt="沙丘" class="w-full h-80 object-cover transition-transform duration-500 group-hover:scale-110">
                <div class="absolute inset-0 bg-gradient-to-t from-dark via-dark/40 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                  <div class="flex items-center justify-between">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">8.7</span>
                    </div>
                    <div class="flex space-x-2">
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-play"></i>
                      </button>
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-plus"></i>
                      </button>
                    </div>
                  </div>
                </div>
                <div class="absolute top-2 right-2">
                  <span class="px-2 py-1 bg-accent text-white text-xs font-bold rounded">9.1</span>
                </div>
              </div>
              <h3 class="font-bold text-white">沙丘</h3>
              <p class="text-white/70 text-sm">2021 • 科幻/冒险</p>
            </div>
            
            <!-- 电影卡片2 -->
            <div class="movie-card w-64 flex-shrink-0 group">
              <div class="relative rounded-xl overflow-hidden mb-3">
                <img src="https://picsum.photos/id/1019/300/450" alt="星际穿越" class="w-full h-80 object-cover transition-transform duration-500 group-hover:scale-110">
                <div class="absolute inset-0 bg-gradient-to-t from-dark via-dark/40 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                  <div class="flex items-center justify-between">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">9.4</span>
                    </div>
                    <div class="flex space-x-2">
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-play"></i>
                      </button>
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-plus"></i>
                      </button>
                    </div>
                  </div>
                </div>
                <div class="absolute top-2 right-2">
                  <span class="px-2 py-1 bg-accent text-white text-xs font-bold rounded">9.4</span>
                </div>
              </div>
              <h3 class="font-bold text-white">星际穿越</h3>
              <p class="text-white/70 text-sm">2014 • 科幻/冒险</p>
            </div>
            
            <!-- 电影卡片3 -->
            <div class="movie-card w-64 flex-shrink-0 group">
              <div class="relative rounded-xl overflow-hidden mb-3">
                <img src="https://picsum.photos/id/1029/300/450" alt="阿凡达" class="w-full h-80 object-cover transition-transform duration-500 group-hover:scale-110">
                <div class="absolute inset-0 bg-gradient-to-t from-dark via-dark/40 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                  <div class="flex items-center justify-between">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">8.9</span>
                    </div>
                    <div class="flex space-x-2">
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-play"></i>
                      </button>
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-plus"></i>
                      </button>
                    </div>
                  </div>
                </div>
                <div class="absolute top-2 right-2">
                  <span class="px-2 py-1 bg-accent text-white text-xs font-bold rounded">8.9</span>
                </div>
              </div>
              <h3 class="font-bold text-white">阿凡达</h3>
              <p class="text-white/70 text-sm">2009 • 科幻/冒险</p>
            </div>
            
            <!-- 电影卡片4 -->
            <div class="movie-card w-64 flex-shrink-0 group">
              <div class="relative rounded-xl overflow-hidden mb-3">
                <img src="https://picsum.photos/id/1074/300/450" alt="盗梦空间" class="w-full h-80 object-cover transition-transform duration-500 group-hover:scale-110">
                <div class="absolute inset-0 bg-gradient-to-t from-dark via-dark/40 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                  <div class="flex items-center justify-between">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">9.0</span>
                    </div>
                    <div class="flex space-x-2">
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-play"></i>
                      </button>
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-plus"></i>
                      </button>
                    </div>
                  </div>
                </div>
                <div class="absolute top-2 right-2">
                  <span class="px-2 py-1 bg-accent text-white text-xs font-bold rounded">9.0</span>
                </div>
              </div>
              <h3 class="font-bold text-white">盗梦空间</h3>
              <p class="text-white/70 text-sm">2010 • 科幻/悬疑</p>
            </div>
            
            <!-- 电影卡片5 -->
            <div class="movie-card w-64 flex-shrink-0 group">
              <div class="relative rounded-xl overflow-hidden mb-3">
                <img src="https://picsum.photos/id/1079/300/450" alt="2001太空漫游" class="w-full h-80 object-cover transition-transform duration-500 group-hover:scale-110">
                <div class="absolute inset-0 bg-gradient-to-t from-dark via-dark/40 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                  <div class="flex items-center justify-between">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">8.8</span>
                    </div>
                    <div class="flex space-x-2">
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-play"></i>
                      </button>
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-plus"></i>
                      </button>
                    </div>
                  </div>
                </div>
                <div class="absolute top-2 right-2">
                  <span class="px-2 py-1 bg-accent text-white text-xs font-bold rounded">8.8</span>
                </div>
              </div>
              <h3 class="font-bold text-white">2001太空漫游</h3>
              <p class="text-white/70 text-sm">1968 • 科幻/悬疑</p>
            </div>
            
            <!-- 电影卡片6 -->
            <div class="movie-card w-64 flex-shrink-0 group">
              <div class="relative rounded-xl overflow-hidden mb-3">
                <img src="https://picsum.photos/id/1076/300/450" alt="银翼杀手2049" class="w-full h-80 object-cover transition-transform duration-500 group-hover:scale-110">
                <div class="absolute inset-0 bg-gradient-to-t from-dark via-dark/40 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                  <div class="flex items-center justify-between">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">8.5</span>
                    </div>
                    <div class="flex space-x-2">
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-play"></i>
                      </button>
                      <button class="w-8 h-8 rounded-full bg-darker/80 flex items-center justify-center text-white hover:bg-primary/80 transition-all duration-300">
                        <i class="fa fa-plus"></i>
                      </button>
                    </div>
                  </div>
                </div>
                <div class="absolute top-2 right-2">
                  <span class="px-2 py-1 bg-accent text-white text-xs font-bold rounded">8.5</span>
                </div>
              </div>
              <h3 class="font-bold text-white">银翼杀手2049</h3>
              <p class="text-white/70 text-sm">2017 • 科幻/悬疑</p>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- 即将上映 -->
    <section class="container mx-auto px-4 mb-16">
      <h2 class="text-2xl font-display font-bold text-white mb-6">即将上映</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <!-- 即将上映电影 1 -->
        <div class="bg-darker/60 backdrop-blur-xl rounded-2xl overflow-hidden border border-primary/20 transition-all duration-500 hover:border-secondary/50 hover:shadow-lg hover:shadow-primary/10 transform hover:-translate-y-2 movie-detail-btn" data-id="2">
          <div class="relative">
            <img src="https://picsum.photos/id/1071/600/300" alt="沙丘2" class="w-full h-48 object-cover">
            <div class="absolute top-0 right-0 bg-accent text-white px-3 py-1 text-sm font-bold">
              2025-07-20 上映
            </div>
          </div>
          <div class="p-6">
            <h3 class="text-xl font-bold mb-2">沙丘2</h3>
            <div class="flex items-center space-x-4 mb-4">
              <div class="flex items-center">
                <i class="fa fa-star text-yellow-400 mr-1"></i>
                <span class="font-bold">9.1 (预售)</span>
              </div>
              <span class="text-white/70">|</span>
              <span>科幻 / 冒险</span>
            </div>
            <p class="text-white/70 mb-6 line-clamp-3">
              保罗·厄崔迪与契尼联手，为了复仇与生存，必须与哈克南男爵展开终极对决，同时还要面对宇宙中更强大的威胁...
            </p>
            <div class="flex justify-between items-center">
              <button class="px-4 py-2 bg-primary/20 border border-primary/30 text-secondary rounded-lg hover:bg-primary/30 transition-all duration-300">
                预约提醒
              </button>
              <span class="text-white/50 text-sm">距离上映还有 35 天</span>
            </div>
          </div>
        </div>
        
        <!-- 即将上映电影 2 -->
        <div class="bg-darker/60 backdrop-blur-xl rounded-2xl overflow-hidden border border-primary/20 transition-all duration-500 hover:border-secondary/50 hover:shadow-lg hover:shadow-primary/10 transform hover:-translate-y-2 movie-detail-btn" data-id="3">
          <div class="relative">
            <img src="https://picsum.photos/id/1072/600/300" alt="星际迷航：奇异新世界" class="w-full h-48 object-cover">
            <div class="absolute top-0 right-0 bg-accent text-white px-3 py-1 text-sm font-bold">
              2025-09-15 上映
            </div>
          </div>
          <div class="p-6">
            <h3 class="text-xl font-bold mb-2">星际迷航：奇异新世界</h3>
            <div class="flex items-center space-x-4 mb-4">
              <div class="flex items-center">
                <i class="fa fa-star text-yellow-400 mr-1"></i>
                <span class="font-bold">8.9 (预售)</span>
              </div>
              <span class="text-white/70">|</span>
              <span>科幻 / 冒险</span>
            </div>
            <p class="text-white/70 mb-6 line-clamp-3">
              企业号船员们踏上新的航程，探索未知的星系，面对神秘的外星文明，同时揭开宇宙中隐藏的秘密...
            </p>
            <div class="flex justify-between items-center">
              <button class="px-4 py-2 bg-primary/20 border border-primary/30 text-secondary rounded-lg hover:bg-primary/30 transition-all duration-300">
                预约提醒
              </button>
              <span class="text-white/50 text-sm">距离上映还有 92 天</span>
            </div>
          </div>
        </div>
        
        <!-- 即将上映电影 3 -->
        <div class="bg-darker/60 backdrop-blur-xl rounded-2xl overflow-hidden border border-primary/20 transition-all duration-500 hover:border-secondary/50 hover:shadow-lg hover:shadow-primary/10 transform hover:-translate-y-2 movie-detail-btn" data-id="4">
          <div class="relative">
            <img src="https://picsum.photos/id/1073/600/300" alt="阿凡达3" class="w-full h-48 object-cover">
            <div class="absolute top-0 right-0 bg-accent text-white px-3 py-1 text-sm font-bold">
              2026-03-01 上映
            </div>
          </div>
          <div class="p-6">
            <h3 class="text-xl font-bold mb-2">阿凡达3</h3>
            <div class="flex items-center space-x-4 mb-4">
              <div class="flex items-center">
                <i class="fa fa-star text-yellow-400 mr-1"></i>
                <span class="font-bold">9.2 (预售)</span>
              </div>
              <span class="text-white/70">|</span>
              <span>科幻 / 冒险</span>
            </div>
            <p class="text-white/70 mb-6 line-clamp-3">
              杰克·萨利与妮特丽继续守护潘多拉星球，面对人类的再次入侵，他们必须联合各部落，为生存而战...
            </p>
            <div class="flex justify-between items-center">
              <button class="px-4 py-2 bg-primary/20 border border-primary/30 text-secondary rounded-lg hover:bg-primary/30 transition-all duration-300">
                预约提醒
              </button>
              <span class="text-white/50 text-sm">距离上映还有 260 天</span>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- 用户评分与统计 -->
    <section class="container mx-auto px-4 mb-16">
      <div class="flex flex-col md:flex-row justify-between items-center mb-8">
        <h2 class="text-2xl font-display font-bold text-white mb-4 md:mb-0">用户评分趋势</h2>
        <div class="flex space-x-2">
          <button class="px-4 py-2 bg-darker/80 border border-primary/30 rounded-lg text-white hover:border-secondary transition-all duration-300">月度</button>
          <button class="px-4 py-2 bg-primary text-white rounded-lg">季度</button>
          <button class="px-4 py-2 bg-darker/80 border border-primary/30 rounded-lg text-white hover:border-secondary transition-all duration-300">年度</button>
        </div>
      </div>
      
      <div class="bg-darker/60 backdrop-blur-xl rounded-2xl p-6 border border-primary/20">
        <div class="h-80">
          <canvas id="ratingsChart"></canvas>
        </div>
      </div>
    </section>
    
    <!-- 订阅区域 -->
    <section class="container mx-auto px-4 mb-16 relative overflow-hidden rounded-3xl">
      <div class="absolute inset-0">
        <img src="https://picsum.photos/id/1002/1920/800" alt="背景" class="w-full h-full object-cover">
        <div class="absolute inset-0 bg-gradient-to-r from-dark via-dark/80 to-dark/60"></div>
      </div>
      
      <div class="relative z-10 py-16 px-8 md:px-16 flex flex-col md:flex-row items-center justify-between">
        <div class="max-w-2xl mb-8 md:mb-0">
          <h2 class="text-3xl md:text-4xl font-display font-bold text-white mb-4">订阅我们的电影资讯</h2>
          <p class="text-white/80 text-lg mb-6">
            第一时间获取最新电影资讯、独家预告片和限时优惠，不错过任何精彩内容。
          </p>
          <div class="flex flex-col sm:flex-row gap-4">
            <input 
              type="email" 
              placeholder="输入你的邮箱地址" 
              class="flex-grow px-4 py-3 bg-darker/80 border border-primary/30 rounded-lg text-white focus:outline-none focus:border-secondary transition-all duration-300"
            >
            <button class="px-6 py-3 bg-gradient-to-r from-primary to-secondary text-white font-bold rounded-lg hover:shadow-lg hover:shadow-primary/30 transition-all duration-300 whitespace-nowrap">
              立即订阅
            </button>
          </div>
        </div>
        
        <div class="hidden md:block w-1/3">
          <div class="relative">
            <img 
              src="https://picsum.photos/id/1025/500/500" 
              alt="电影" 
              class="w-full h-auto rounded-2xl border-4 border-primary/30 animate-float"
            >
            <div class="absolute -bottom-4 -right-4 w-24 h-24 bg-accent rounded-full flex items-center justify-center text-white font-bold text-2xl animate-pulse-slow">
              <span>新</span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>

  <!-- 页脚 -->
  <footer class="bg-darker border-t border-primary/20">
    <div class="container mx-auto px-4 py-12">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
        <div>
          <div class="flex items-center space-x-2 mb-6">
            <div class="w-10 h-10 rounded-full bg-gradient-to-r from-primary to-secondary flex items-center justify-center">
              <i class="fa fa-film text-white text-xl"></i>
            </div>
            <h2 class="text-2xl font-display font-bold text-shadow-glow">星际电影</h2>
          </div>
          <p class="text-white/70 mb-6">
            探索奇幻影视世界，发现无限可能。我们提供最新、最热门的电影推荐，满足你的观影需求。
          </p>
          <div class="flex space-x-4">
            <a href="#" class="w-10 h-10 rounded-full bg-dark/80 flex items-center justify-center text-white hover:bg-primary/20 transition-all duration-300">
              <i class="fa fa-facebook"></i>
            </a>
            <a href="#" class="w-10 h-10 rounded-full bg-dark/80 flex items-center justify-center text-white hover:bg-primary/20 transition-all duration-300">
              <i class="fa fa-twitter"></i>
            </a>
            <a href="#" class="w-10 h-10 rounded-full bg-dark/80 flex items-center justify-center text-white hover:bg-primary/20 transition-all duration-300">
              <i class="fa fa-instagram"></i>
            </a>
            <a href="#" class="w-10 h-10 rounded-full bg-dark/80 flex items-center justify-center text-white hover:bg-primary/20 transition-all duration-300">
              <i class="fa fa-youtube-play"></i>
            </a>
          </div>
        </div>
        
        <div>
          <h3 class="text-xl font-bold mb-6">快速链接</h3>
          <ul class="space-y-3">
            <li><a href="index.html" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 首页
            </a></li>
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 电影分类
            </a></li>
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 排行榜
            </a></li>
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 最新上映
            </a></li>
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 关于我们
            </a></li>
          </ul>
        </div>
        
        <div>
          <h3 class="text-xl font-bold mb-6">支持</h3>
          <ul class="space-y-3">
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 帮助中心
            </a></li>
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 常见问题
            </a></li>
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 联系我们
            </a></li>
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 隐私政策
            </a></li>
            <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
              <i class="fa fa-angle-right mr-2"></i> 使用条款
            </a></li>
          </ul>
        </div>
        
        <div>
          <h3 class="text-xl font-bold mb-6">联系我们</h3>
          <ul class="space-y-3">
            <li class="flex items-start space-x-3">
              <i class="fa fa-map-marker text-secondary mt-1"></i>
              <span class="text-white/70">北京市朝阳区科幻大道1001号星际中心</span>
            </li>
            <li class="flex items-center space-x-3">
              <i class="fa fa-phone text-secondary"></i>
              <span class="text-white/70">+86 10 8888 8888</span>
            </li>
            <li class="flex items-center space-x-3">
              <i class="fa fa-envelope text-secondary"></i>
              <span class="text-white/70">contact@xingjimov.com</span>
            </li>
          </ul>
          
          <div class="mt-6">
            <h4 class="text-lg font-bold mb-3">下载我们的应用</h4>
            <div class="flex space-x-3">
                            <a href="#" class="bg-dark/80 rounded-lg p-2 hover:bg-primary/20 transition-all duration-300">
                              <i class="fa fa-apple text-2xl"></i>
                            </a>
                            <a href="#" class="bg-dark/80 rounded-lg p-2 hover:bg-primary/20 transition-all duration-300">
                              <i class="fa fa-android text-2xl"></i>
                            </a>
                          </div>
                        </div>
                      </div>
                    </div>
                    
                    <div class="border-t border-gray-800 mt-12 pt-8 text-center text-white/50 text-sm">
                      <p>© 2025 星际电影推荐. 保留所有权利.</p>
                    </div>
                  </div>
                </footer>
              
                <!-- 预告片模态框 -->
                <div class="fixed inset-0 z-50 flex items-center justify-center hidden" id="trailerModal">
                  <div class="absolute inset-0 bg-black/80 backdrop-blur-sm" id="modalOverlay"></div>
                  <div class="relative bg-darker rounded-2xl max-w-4xl w-full max-h-[90vh] overflow-hidden border-4 border-primary/30 transform transition-all duration-500 scale-95 opacity-0" id="modalContent">
                    <button class="absolute top-4 right-4 text-white/70 hover:text-white transition-colors text-2xl z-10" id="closeTrailerModal">
                      <i class="fa fa-times"></i>
                    </button>
                    
                    <div class="aspect-w-16 aspect-h-9">
                      <iframe 
                        id="trailerIframe" 
                        src="https://www.youtube.com/embed/d9vyBHfW9d0" 
                        title="电影预告片" 
                        frameborder="0" 
                        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
                        allowfullscreen
                        class="w-full h-full"
                      ></iframe>
                    </div>
                  </div>
                </div>
              
                <!-- 搜索结果模态框 -->
                <div class="fixed inset-0 z-50 flex items-center justify-center hidden" id="searchModal">
                  <div class="absolute inset-0 bg-black/80 backdrop-blur-sm" id="searchOverlay"></div>
                  <div class="relative bg-darker rounded-2xl max-w-3xl w-full max-h-[90vh] overflow-y-auto border-4 border-primary/30 transform transition-all duration-500 scale-95 opacity-0" id="searchContent">
                    <div class="p-6">
                      <div class="flex justify-between items-center mb-6">
                        <h2 class="text-2xl font-bold text-white">搜索结果</h2>
                        <button class="text-white/70 hover:text-white transition-colors" id="closeSearchModal">
                          <i class="fa fa-times"></i>
                        </button>
                      </div>
                      
                      <div class="relative mb-6">
                        <input 
                          type="text" 
                          id="searchInputModal" 
                          placeholder="继续搜索..." 
                          class="w-full bg-dark border border-primary/30 rounded-full py-2 pl-10 pr-4 focus:outline-none focus:border-secondary transition-all duration-300"
                        >
                        <i class="fa fa-search absolute left-3 top-3 text-primary"></i>
                      </div>
                      
                      <div class="space-y-4" id="searchResults">
                        <!-- 搜索结果将通过JavaScript动态生成 -->
                        <div class="search-result flex space-x-4 p-3 hover:bg-primary/10 rounded-lg transition-colors">
                          <img src="https://picsum.photos/id/1019/100/150" alt="星际穿越" class="w-20 h-30 object-cover rounded-lg">
                          <div class="flex-grow">
                            <h3 class="font-bold text-white">星际穿越</h3>
                            <div class="flex items-center text-white/70 text-sm mt-1">
                              <span>科幻 / 冒险</span>
                              <span class="mx-2">•</span>
                              <span>9.4分</span>
                            </div>
                          </div>
                        </div>
                        
                        <div class="search-result flex space-x-4 p-3 hover:bg-primary/10 rounded-lg transition-colors">
                          <img src="https://picsum.photos/id/1025/100/150" alt="沙丘" class="w-20 h-30 object-cover rounded-lg">
                          <div class="flex-grow">
                            <h3 class="font-bold text-white">沙丘</h3>
                            <div class="flex items-center text-white/70 text-sm mt-1">
                              <span>科幻 / 冒险</span>
                              <span class="mx-2">•</span>
                              <span>8.7分</span>
                            </div>
                          </div>
                        </div>
                        
                        <div class="search-result flex space-x-4 p-3 hover:bg-primary/10 rounded-lg transition-colors">
                          <img src="https://picsum.photos/id/1029/100/150" alt="阿凡达" class="w-20 h-30 object-cover rounded-lg">
                          <div class="flex-grow">
                            <h3 class="font-bold text-white">阿凡达</h3>
                            <div class="flex items-center text-white/70 text-sm mt-1">
                              <span>科幻 / 冒险</span>
                              <span class="mx-2">•</span>
                              <span>8.9分</span>
                            </div>
                          </div>
                        </div>
                      </div>
                      
                      <div class="text-center mt-6">
                        <button class="px-6 py-2 bg-dark border border-primary/30 rounded-lg text-white hover:border-secondary transition-all duration-300">
                          查看更多搜索结果
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
              
                <!-- JavaScript -->
                <script>
                  // 生成背景星星
                  function createStars() {
                    const stars = document.getElementById('stars');
                    const count = 200;
                    
                    for (let i = 0; i < count; i++) {
                      const star = document.createElement('div');
                      const size = Math.random() * 3 + 1;
                      const opacity = Math.random() * 0.8 + 0.2;
                      const x = Math.random() * 100;
                      const y = Math.random() * 100;
                      const duration = Math.random() * 10 + 5;
                      
                      star.style.cssText = `
                        position: absolute;
                        width: ${size}px;
                        height: ${size}px;
                        background: rgba(255, 255, 255, ${opacity});
                        border-radius: 50%;
                        left: ${x}%;
                        top: ${y}%;
                        box-shadow: 0 0 ${size}px rgba(255, 255, 255, 0.8);
                        animation: blink ${duration}s infinite ease-in-out;
                      `;
                      
                      stars.appendChild(star);
                    }
                  }
                  
                  // 导航栏滚动效果
                  const navbar = document.getElementById('navbar');
                  
                  window.addEventListener('scroll', () => {
                    if (window.scrollY > 100) {
                      navbar.classList.add('py-2', 'shadow-lg');
                      navbar.classList.remove('py-4');
                    } else {
                      navbar.classList.add('py-4');
                      navbar.classList.remove('py-2', 'shadow-lg');
                    }
                  });
                  
                  // 移动端菜单切换
                  const mobileMenuBtn = document.getElementById('mobileMenuBtn');
                  const mobileMenu = document.getElementById('mobileMenu');
                  
                  mobileMenuBtn.addEventListener('click', () => {
                    mobileMenu.classList.toggle('hidden');
                    mobileMenuBtn.innerHTML = mobileMenu.classList.contains('hidden') 
                      ? '<i class="fa fa-bars"></i>' 
                      : '<i class="fa fa-times"></i>';
                  });
                  
                  // 用户菜单切换
                  const userMenuBtn = document.getElementById('userMenuBtn');
                  const userMenu = document.getElementById('userMenu');
                  
                  userMenuBtn.addEventListener('click', (e) => {
                    e.stopPropagation();
                    userMenu.classList.toggle('hidden');
                  });
                  
                  // 点击其他地方关闭用户菜单
                  document.addEventListener('click', () => {
                    userMenu.classList.add('hidden');
                  });
                  
                  // 阻止用户菜单项点击事件冒泡
                  userMenu.addEventListener('click', (e) => {
                    e.stopPropagation();
                  });
                  
                  // 热门电影滚动控制
                  const hotMovies = document.getElementById('hotMovies');
                  const prevHot = document.getElementById('prevHot');
                  const nextHot = document.getElementById('nextHot');
                  
                  nextHot.addEventListener('click', () => {
                    hotMovies.scrollBy({ left: 300, behavior: 'smooth' });
                  });
                  
                  prevHot.addEventListener('click', () => {
                    hotMovies.scrollBy({ left: -300, behavior: 'smooth' });
                  });
                  
                  // 评分图表
                  const ctx = document.getElementById('ratingsChart').getContext('2d');
                  const ratingsChart = new Chart(ctx, {
                    type: 'line',
                    data: {
                      labels: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月'],
                      datasets: [
                        {
                          label: '科幻',
                          data: [9.2, 9.1, 9.3, 9.4, 9.3, 9.5, 9.4, 9.5, 9.6],
                          borderColor: '#6C5CE7',
                          backgroundColor: 'rgba(108, 92, 231, 0.1)',
                          tension: 0.4,
                          fill: true
                        },
                        {
                          label: '动作',
                          data: [8.7, 8.8, 8.9, 8.8, 9.0, 8.9, 9.1, 9.0, 9.2],
                          borderColor: '#00CEFF',
                          backgroundColor: 'rgba(0, 206, 255, 0.1)',
                          tension: 0.4,
                          fill: true
                        },
                        {
                          label: '奇幻',
                          data: [8.5, 8.6, 8.7, 8.8, 8.9, 9.0, 9.1, 9.2, 9.3],
                          borderColor: '#FF2E63',
                          backgroundColor: 'rgba(255, 46, 99, 0.1)',
                          tension: 0.4,
                          fill: true
                        }
                      ]
                    },
                    options: {
                      responsive: true,
                      maintainAspectRatio: false,
                      plugins: {
                        legend: {
                          position: 'top',
                          labels: {
                            color: 'rgba(255, 255, 255, 0.7)',
                            font: {
                              family: 'Inter',
                              size: 12
                            }
                          }
                        },
                        tooltip: {
                          mode: 'index',
                          intersect: false,
                          backgroundColor: 'rgba(10, 8, 20, 0.9)',
                          titleColor: '#fff',
                          bodyColor: 'rgba(255, 255, 255, 0.7)',
                          borderColor: 'rgba(108, 92, 231, 0.3)',
                          borderWidth: 1,
                          padding: 12,
                          displayColors: false,
                          callbacks: {
                            label: function(context) {
                              return ` ${context.dataset.label}: ${context.raw}`;
                            }
                          }
                        }
                      },
                      scales: {
                        x: {
                          grid: {
                            display: false,
                            drawBorder: false
                          },
                          ticks: {
                            color: 'rgba(255, 255, 255, 0.5)'
                          }
                        },
                        y: {
                          min: 8,
                          max: 10,
                          grid: {
                            color: 'rgba(255, 255, 255, 0.05)',
                            drawBorder: false
                          },
                          ticks: {
                            color: 'rgba(255, 255, 255, 0.5)',
                            stepSize: 0.5
                          }
                        }
                      },
                      interaction: {
                        mode: 'nearest',
                        axis: 'x',
                        intersect: false
                      },
                      elements: {
                        point: {
                          radius: 2,
                          hoverRadius: 5,
                          backgroundColor: '#fff'
                        }
                      }
                    }
                  });
                  
                  // 预告片模态框
                  const trailerModal = document.getElementById('trailerModal');
                  const modalContent = document.getElementById('modalContent');
                  const modalOverlay = document.getElementById('modalOverlay');
                  const closeTrailerModal = document.getElementById('closeTrailerModal');
                  const trailerIframe = document.getElementById('trailerIframe');
                  const movieDetailBtns = document.querySelectorAll('.movie-detail-btn');
                  
                  function openTrailerModal() {
                    trailerModal.classList.remove('hidden');
                    setTimeout(() => {
                      modalContent.classList.remove('scale-95', 'opacity-0');
                      modalContent.classList.add('scale-100', 'opacity-100');
                    }, 10);
                    
                    // 延迟加载iframe内容，避免闪烁
                    setTimeout(() => {
                      const src = trailerIframe.src;
                      trailerIframe.src = '';
                      trailerIframe.src = src;
                    }, 50);
                  }
                  
                  function closeTrailerModalFunc() {
                    modalContent.classList.remove('scale-100', 'opacity-100');
                    modalContent.classList.add('scale-95', 'opacity-0');
                    setTimeout(() => {
                      trailerModal.classList.add('hidden');
                    }, 300);
                  }
                  
                  // 点击电影详情按钮打开预告片模态框
                  movieDetailBtns.forEach(btn => {
                    btn.addEventListener('click', openTrailerModal);
                  });
                  
                  closeTrailerModal.addEventListener('click', closeTrailerModalFunc);
                  modalOverlay.addEventListener('click', closeTrailerModalFunc);
                  
                  // 搜索功能
                  const searchInput = document.getElementById('searchInput');
                  const searchModal = document.getElementById('searchModal');
                  const searchContent = document.getElementById('searchContent');
                  const searchOverlay = document.getElementById('searchOverlay');
                  const closeSearchModal = document.getElementById('closeSearchModal');
                  const searchInputModal = document.getElementById('searchInputModal');
                  const searchResults = document.getElementById('searchResults');
                  
                  function openSearchModal() {
                    searchModal.classList.remove('hidden');
                    setTimeout(() => {
                      searchContent.classList.remove('scale-95', 'opacity-0');
                      searchContent.classList.add('scale-100', 'opacity-100');
                      searchInputModal.focus();
                    }, 10);
                  }
                  
                  function closeSearchModalFunc() {
                    searchContent.classList.remove('scale-100', 'opacity-100');
                    searchContent.classList.add('scale-95', 'opacity-0');
                    setTimeout(() => {
                      searchModal.classList.add('hidden');
                    }, 300);
                  }
                  
                  // 点击搜索框打开搜索模态框
                  searchInput.addEventListener('click', openSearchModal);
                  
                  // 模态框内的搜索框回车事件
                  searchInputModal.addEventListener('keypress', (e) => {
                    if (e.key === 'Enter') {
                      // 这里可以添加搜索逻辑
                      console.log('搜索:', searchInputModal.value);
                    }
                  });
                  
                  closeSearchModal.addEventListener('click', closeSearchModalFunc);
                  searchOverlay.addEventListener('click', closeSearchModalFunc);
                  
                  // 搜索结果点击事件（模拟跳转到电影详情页）
                  document.querySelectorAll('.search-result').forEach(result => {
                    result.addEventListener('click', openTrailerModal);
                  });
                  
                  // 页面跳转逻辑（模拟）
                  document.querySelectorAll('a[href^="index.html"], .movie-card, .category-card').forEach(link => {
                    link.addEventListener('click', (e) => {
                      e.preventDefault();
                      // 这里可以添加实际的页面跳转逻辑
                      // 例如：window.location.href = 'movie-detail.html?id=1';
                      openTrailerModal();
                    });
                  });
                  
                  // 通知按钮点击事件
                  const notificationBtn = document.getElementById('notificationBtn');
                  notificationBtn.addEventListener('click', () => {
                    // 这里可以添加通知面板的逻辑
                    alert('通知功能将在后续版本中实现');
                  });
                  
                  // 书签按钮点击事件
                  const bookmarkBtn = document.getElementById('bookmarkBtn');
                  bookmarkBtn.addEventListener('click', () => {
                    // 切换书签状态
                    bookmarkBtn.innerHTML = bookmarkBtn.innerHTML.includes('bookmark-o') 
                      ? '<i class="fa fa-bookmark text-primary"></i>' 
                      : '<i class="fa fa-bookmark-o text-white"></i>';
                  });
                  
                  // 初始化
                  window.addEventListener('load', () => {
                    createStars();
                    
                    // 模拟加载动画
                    setTimeout(() => {
                      document.body.classList.add('loaded');
                    }, 500);
                  });
                </script>
              </body>
              </html>
