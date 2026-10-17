<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kizaru's Rusty Clips</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Google Fonts: Inter -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
  
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            rust: {
              50: '#fffbeb',
              100: '#fef3c7',
              400: '#fbbf24',
              500: '#f59e0b',
              600: '#d97706',
              700: '#b45309',
              800: '#92400e',
              900: '#78350f',
              950: '#451a03',
            },
            metal: {
              800: '#1e2025',
              850: '#17191d',
              900: '#111215',
              950: '#0b0c0e',
            }
          },
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
          }
        }
      }
    }
  </script>

  <style>
    /* Custom Scrollbar for Rusty Aesthetic */
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #111215;
    }
    ::-webkit-scrollbar-thumb {
      background: #2d3038;
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #d97706;
    }
    
    .rust-glow {
      box-shadow: 0 0 15px rgba(217, 119, 6, 0.25);
    }
    .rust-text-glow {
      text-shadow: 0 0 10px rgba(217, 119, 6, 0.4);
    }
  </style>
</head>
<body class="bg-metal-950 text-gray-100 font-sans antialiased min-h-screen flex flex-col selection:bg-rust-600 selection:text-white">

  <!-- ================= HEADER / NAVBAR ================= -->
  <header class="sticky top-0 z-40 bg-metal-900/95 backdrop-blur-md border-b border-metal-800 px-4 py-2.5 flex items-center justify-between gap-4">
    
    <!-- Left: Menu & Brand -->
    <div class="flex items-center gap-3">
      <button id="toggleSidebar" class="p-2 text-gray-400 hover:text-white rounded-lg hover:bg-metal-800 transition">
        <i class="fa-solid fa-bars text-lg"></i>
      </button>
      <a href="#" id="brandLogo" class="flex items-center gap-2 group">
        <div class="w-9 h-9 rounded-xl bg-gradient-to-tr from-rust-700 via-rust-600 to-amber-500 flex items-center justify-center text-white shadow-lg shadow-rust-900/50 group-hover:scale-105 transition transform">
          <i class="fa-solid fa-bolt text-lg"></i>
        </div>
        <div class="flex flex-col">
          <span class="font-extrabold text-lg tracking-tight bg-gradient-to-r from-amber-400 via-rust-500 to-amber-200 bg-clip-text text-transparent group-hover:rust-text-glow transition">
            KIZARU'S
          </span>
          <span class="text-[10px] font-bold tracking-widest text-rust-500 -mt-1.5 uppercase">Rusty Clips</span>
        </div>
      </a>
    </div>

    <!-- Center: Search Bar -->
    <div class="flex-1 max-w-2xl mx-2 hidden sm:flex items-center">
      <div class="relative w-full flex items-center">
        <input type="text" id="searchInput" placeholder="Search rusty clips, gaming, memes..." 
               class="w-full bg-metal-950 border border-metal-800 text-gray-200 text-sm rounded-l-full py-2 pl-4 pr-10 focus:outline-none focus:border-rust-600 focus:ring-1 focus:ring-rust-600 transition placeholder-gray-500">
        <button id="clearSearch" class="hidden absolute right-14 text-gray-500 hover:text-gray-300">
          <i class="fa-solid fa-xmark"></i>
        </button>
        <button id="searchBtn" class="bg-metal-800 hover:bg-metal-800/80 border border-l-0 border-metal-800 text-gray-300 hover:text-rust-500 px-5 py-2 rounded-r-full transition flex items-center justify-center">
          <i class="fa-solid fa-magnifying-glass"></i>
        </button>
      </div>
    </div>

    <!-- Right: Actions & User -->
    <div class="flex items-center gap-2 sm:gap-3">
      <button id="mobileSearchBtn" class="sm:hidden p-2 text-gray-400 hover:text-white rounded-full hover:bg-metal-800">
        <i class="fa-solid fa-magnifying-glass text-lg"></i>
      </button>

      <!-- Upload Button -->
      <button id="openUploadModal" class="flex items-center gap-2 bg-gradient-to-r from-rust-700 to-rust-600 hover:from-rust-600 hover:to-rust-500 text-white text-xs sm:text-sm font-semibold px-3 sm:px-4 py-2 rounded-full transition shadow-md shadow-rust-950/40 border border-rust-500/30">
        <i class="fa-solid fa-cloud-arrow-up"></i>
        <span class="hidden sm:inline">Upload Clip</span>
      </button>

      <!-- Notifications -->
      <button class="p-2 text-gray-400 hover:text-white rounded-full hover:bg-metal-800 relative">
        <i class="fa-solid fa-bell text-lg"></i>
        <span class="absolute top-1.5 right-1.5 w-2 h-2 bg-rust-500 rounded-full animate-pulse"></span>
      </button>

      <!-- User Avatar -->
      <div class="w-8 h-8 rounded-full bg-gradient-to-br from-rust-600 to-metal-800 border border-rust-500/40 flex items-center justify-center text-xs font-bold text-amber-200 cursor-pointer hover:ring-2 hover:ring-rust-500 transition">
        KZ
      </div>
    </div>
  </header>

  <!-- Mobile Search Drawer -->
  <div id="mobileSearchBar" class="hidden sm:hidden bg-metal-900 px-4 py-3 border-b border-metal-800">
    <div class="flex items-center gap-2">
      <input type="text" id="mobileSearchInput" placeholder="Search clips..." 
             class="w-full bg-metal-950 border border-metal-800 text-gray-200 text-sm rounded-full py-2 px-4 focus:outline-none focus:border-rust-600">
      <button id="closeMobileSearch" class="p-2 text-gray-400">
        <i class="fa-solid fa-xmark text-lg"></i>
      </button>
    </div>
  </div>

  <!-- ================= MAIN CONTENT WRAPPER ================= -->
  <div class="flex-1 flex overflow-hidden">

    <!-- SIDEBAR NAVIGATION -->
    <aside id="sidebar" class="w-64 bg-metal-900/80 border-r border-metal-800/80 flex-shrink-0 flex flex-col justify-between transition-all duration-300 z-30 fixed lg:relative inset-y-0 left-0 transform -translate-x-full lg:translate-x-0 pt-14 lg:pt-0">
      <div class="p-3 space-y-6 overflow-y-auto max-h-full">
        <!-- Main Links -->
        <div class="space-y-1">
          <button data-nav="home" class="nav-item active flex items-center gap-4 w-full px-3 py-2.5 rounded-xl text-sm font-medium transition text-rust-500 bg-rust-500/10 border border-rust-500/20">
            <i class="fa-solid fa-house text-lg w-5 text-center"></i>
            <span>Home</span>
          </button>
          <button data-nav="trending" class="nav-item flex items-center gap-4 w-full px-3 py-2.5 rounded-xl text-sm font-medium text-gray-400 hover:text-gray-100 hover:bg-metal-800 transition">
            <i class="fa-solid fa-fire text-lg w-5 text-center"></i>
            <span>Trending Clips</span>
          </button>
          <button data-nav="subscriptions" class="nav-item flex items-center gap-4 w-full px-3 py-2.5 rounded-xl text-sm font-medium text-gray-400 hover:text-gray-100 hover:bg-metal-800 transition">
            <i class="fa-solid fa-layer-group text-lg w-5 text-center"></i>
            <span>Subscriptions</span>
          </button>
        </div>

        <hr class="border-metal-800">

        <!-- Library Links -->
        <div class="space-y-1">
          <div class="px-3 text-xs font-semibold uppercase text-gray-500 tracking-wider mb-2">Library</div>
          <button data-nav="my-clips" class="nav-item flex items-center gap-4 w-full px-3 py-2.5 rounded-xl text-sm font-medium text-gray-400 hover:text-gray-100 hover:bg-metal-800 transition">
            <i class="fa-solid fa-video text-lg w-5 text-center"></i>
            <span>My Uploaded Clips</span>
          </button>
          <button data-nav="saved" class="nav-item flex items-center gap-4 w-full px-3 py-2.5 rounded-xl text-sm font-medium text-gray-400 hover:text-gray-100 hover:bg-metal-800 transition">
            <i class="fa-solid fa-bookmark text-lg w-5 text-center"></i>
            <span>Saved Clips</span>
          </button>
          <button data-nav="history" class="nav-item flex items-center gap-4 w-full px-3 py-2.5 rounded-xl text-sm font-medium text-gray-400 hover:text-gray-100 hover:bg-metal-800 transition">
            <i class="fa-solid fa-clock-rotate-left text-lg w-5 text-center"></i>
            <span>History</span>
          </button>
        </div>

        <hr class="border-metal-800">

        <!-- Subscriptions Quick List -->
        <div>
          <div class="px-3 text-xs font-semibold uppercase text-gray-500 tracking-wider mb-2">Featured Channels</div>
          <div class="space-y-1">
            <a href="#" class="flex items-center gap-3 px-3 py-2 rounded-xl text-xs font-medium text-gray-400 hover:bg-metal-800 hover:text-gray-200 transition">
              <div class="w-6 h-6 rounded-full bg-rust-700 flex items-center justify-center text-[10px] text-white font-bold">R</div>
              <span class="truncate">Rusty Streamer</span>
            </a>
            <a href="#" class="flex items-center gap-3 px-3 py-2 rounded-xl text-xs font-medium text-gray-400 hover:bg-metal-800 hover:text-gray-200 transition">
              <div class="w-6 h-6 rounded-full bg-amber-600 flex items-center justify-center text-[10px] text-white font-bold">K</div>
              <span class="truncate">Kizaru Highlights</span>
            </a>
          </div>
        </div>
      </div>

      <!-- Footer Info -->
      <div class="p-3 border-t border-metal-800 text-[11px] text-gray-500 space-y-1">
        <p>© 2026 Kizaru's Rusty Clips</p>
        <p class="text-[10px] text-rust-600 font-mono">Rust Engine v2.4.0</p>
      </div>
    </aside>

    <!-- Overlay for Mobile Sidebar -->
    <div id="sidebarOverlay" class="fixed inset-0 bg-black/60 z-20 hidden lg:hidden backdrop-blur-sm"></div>

    <!-- MAIN BODY AREA (FEED OR VIDEO WATCH PAGE) -->
    <main class="flex-1 overflow-y-auto bg-metal-950 p-4 sm:p-6" id="mainContainer">

      <!-- ================= VIEW 1: VIDEO FEED VIEW ================= -->
      <section id="feedView" class="space-y-6">
        
        <!-- Category Filter Tags -->
        <div class="flex items-center gap-2 overflow-x-auto pb-2 scrollbar-none" id="categoryContainer"></div>

        <!-- Section Title Banner -->
        <div class="flex items-center justify-between">
          <h1 id="feedTitle" class="text-xl font-extrabold text-white flex items-center gap-2">
            <i class="fa-solid fa-compass text-rust-500"></i> Explore Clips
          </h1>
          <span id="videoCountBadge" class="text-xs bg-metal-800 text-gray-400 px-3 py-1 rounded-full border border-metal-700">
            0 videos
          </span>
        </div>

        <!-- Video Grid -->
        <div id="videoGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-5 sm:gap-6"></div>

        <!-- Empty State -->
        <div id="emptyFeedState" class="hidden flex-col items-center justify-center py-20 text-center">
          <div class="w-20 h-20 rounded-full bg-metal-900 border border-metal-800 flex items-center justify-center text-rust-500 text-3xl mb-4">
            <i class="fa-solid fa-film"></i>
          </div>
          <h3 class="text-lg font-bold text-gray-200">No clips found</h3>
          <p class="text-sm text-gray-500 max-w-sm mt-1 mb-4">Try adjusting your search query or upload a brand new rusty clip!</p>
          <button id="resetSearchBtn" class="bg-rust-600 hover:bg-rust-500 text-white text-xs font-semibold px-4 py-2 rounded-full transition">
            Clear Filters
          </button>
        </div>

      </section>

      <!-- ================= VIEW 2: VIDEO WATCH PLAYER PAGE ================= -->
      <section id="watchView" class="hidden max-w-7xl mx-auto">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          
          <!-- Left Column: Primary Player & Info -->
          <div class="lg:col-span-2 space-y-4">
            
            <!-- Video Player Box -->
            <div class="relative bg-black rounded-2xl overflow-hidden shadow-2xl border border-metal-800 group">
              <video id="mainVideoPlayer" class="w-full aspect-video object-contain" controls poster="">
                <source src="" type="video/mp4">
                Your browser does not support HTML5 video.
              </video>
            </div>

            <!-- Video Title & Stats -->
            <div class="space-y-3">
              <h1 id="playerTitle" class="text-xl sm:text-2xl font-bold text-white tracking-tight leading-snug"></h1>

              <div class="flex flex-wrap items-center justify-between gap-4 py-1">
                <!-- Channel Info -->
                <div class="flex items-center gap-3">
                  <div id="playerAvatar" class="w-10 h-10 rounded-full bg-rust-700 flex items-center justify-center text-white font-bold text-sm ring-2 ring-rust-600/50"></div>
                  <div>
                    <div id="playerAuthor" class="font-bold text-sm text-gray-100 flex items-center gap-1.5">
                      <i class="fa-solid fa-circle-check text-rust-500 text-xs"></i>
                    </div>
                    <div id="playerSubCount" class="text-xs text-gray-400">12.4K subscribers</div>
                  </div>
                  <button id="subscribeBtn" class="ml-2 bg-rust-600 hover:bg-rust-500 text-white text-xs font-bold px-4 py-2 rounded-full transition shadow-md rust-glow">
                    Subscribe
                  </button>
                </div>

                <!-- Interactive Actions -->
                <div class="flex items-center gap-2 flex-wrap">
                  <div class="flex items-center bg-metal-800 rounded-full p-1 border border-metal-700">
                    <button id="likeBtn" class="flex items-center gap-2 hover:bg-metal-700 text-gray-300 hover:text-rust-500 px-3 py-1.5 rounded-l-full text-xs font-semibold transition">
                      <i class="fa-solid fa-thumbs-up"></i>
                      <span id="likeCount">0</span>
                    </button>
                    <div class="w-[1px] h-4 bg-metal-700"></div>
                    <button id="dislikeBtn" class="flex items-center gap-2 hover:bg-metal-700 text-gray-300 hover:text-red-400 px-3 py-1.5 rounded-r-full text-xs font-semibold transition">
                      <i class="fa-solid fa-thumbs-down"></i>
                      <span id="dislikeCount">0</span>
                    </button>
                  </div>

                  <button id="shareBtn" class="flex items-center gap-2 bg-metal-800 hover:bg-metal-700 border border-metal-700 text-gray-200 text-xs font-semibold px-3.5 py-2 rounded-full transition">
                    <i class="fa-solid fa-share"></i>
                    <span>Share</span>
                  </button>

                  <button id="saveBtn" class="flex items-center gap-2 bg-metal-800 hover:bg-metal-700 border border-metal-700 text-gray-200 text-xs font-semibold px-3.5 py-2 rounded-full transition">
                    <i class="fa-regular fa-bookmark" id="saveIcon"></i>
                    <span id="saveText">Save</span>
                  </button>
                </div>
              </div>

              <!-- Collapsible Description Box -->
              <div class="bg-metal-900 border border-metal-800/80 rounded-xl p-4 space-y-2 text-sm text-gray-300">
                <div class="flex items-center gap-3 text-xs font-bold text-gray-400 border-b border-metal-800 pb-2">
                  <span id="playerViews"></span>
                  <span>•</span>
                  <span id="playerDate"></span>
                  <span id="playerCategoryBadge" class="ml-auto bg-rust-950 text-rust-400 border border-rust-700/50 px-2.5 py-0.5 rounded-md text-[11px] uppercase tracking-wider font-semibold">
                    Gaming
                  </span>
                </div>
                <p id="playerDescription" class="whitespace-pre-line text-sm leading-relaxed text-gray-300"></p>
              </div>

            </div>

            <!-- COMMENTS SECTION -->
            <div class="space-y-4 pt-4 border-t border-metal-800">
              <div class="flex items-center justify-between">
                <h3 class="font-extrabold text-lg text-white flex items-center gap-2">
                  <i class="fa-solid fa-comments text-rust-500"></i>
                  <span>Comments</span>
                  <span id="commentsCountBadge" class="text-xs bg-metal-800 text-gray-400 px-2.5 py-0.5 rounded-full font-normal">0</span>
                </h3>
              </div>

              <!-- Comment Input Box -->
              <div class="flex gap-3 items-start">
                <div class="w-9 h-9 rounded-full bg-rust-600 flex-shrink-0 flex items-center justify-center font-bold text-xs text-amber-100">
                  YOU
                </div>
                <div class="flex-1 space-y-2">
                  <textarea id="commentInput" rows="2" placeholder="Add a rusty comment..." 
                            class="w-full bg-metal-900 border border-metal-800 rounded-xl p-3 text-sm text-gray-200 focus:outline-none focus:border-rust-600 focus:ring-1 focus:ring-rust-600 transition resize-none"></textarea>
                  <div class="flex justify-end gap-2">
                    <button id="cancelCommentBtn" class="text-xs font-medium text-gray-400 hover:text-gray-200 px-3 py-1.5 rounded-lg transition">Cancel</button>
                    <button id="submitCommentBtn" class="bg-rust-600 hover:bg-rust-500 text-white text-xs font-bold px-4 py-1.5 rounded-lg transition shadow-md">
                      Comment
                    </button>
                  </div>
                </div>
              </div>

              <!-- Comments List -->
              <div id="commentsList" class="space-y-4 pt-2"></div>
            </div>

          </div>

          <!-- Right Column: Up Next -->
          <div class="space-y-4">
            <h3 class="font-bold text-base text-gray-200 flex items-center justify-between">
              <span>Up Next</span>
              <span class="text-xs text-rust-500 font-semibold uppercase tracking-wider">Autoplay ON</span>
            </h3>

            <div id="recommendedContainer" class="space-y-3"></div>
          </div>

        </div>
      </section>

    </main>
  </div>

  <!-- ================= MODAL: UPLOAD VIDEO ================= -->
  <div id="uploadModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-md flex items-center justify-center p-4 hidden opacity-0 transition-opacity duration-200">
    <div class="bg-metal-900 border border-metal-800 rounded-2xl max-w-xl w-full p-6 shadow-2xl relative space-y-5 max-h-[90vh] overflow-y-auto">
      
      <button id="closeUploadModal" class="absolute top-4 right-4 text-gray-400 hover:text-white p-2 rounded-lg hover:bg-metal-800 transition">
        <i class="fa-solid fa-xmark text-lg"></i>
      </button>

      <div class="flex items-center gap-3 border-b border-metal-800 pb-4">
        <div class="w-10 h-10 rounded-xl bg-rust-600/20 text-rust-500 border border-rust-500/30 flex items-center justify-center text-xl">
          <i class="fa-solid fa-cloud-arrow-up"></i>
        </div>
        <div>
          <h2 class="text-lg font-bold text-white">Upload to Rusty Clips</h2>
          <p class="text-xs text-gray-400">Share your gameplay, highlights, or meme video</p>
        </div>
      </div>

      <form id="uploadForm" class="space-y-4">
        <div>
          <label class="block text-xs font-semibold uppercase text-gray-400 mb-2">Video Source</label>
          <div class="grid grid-cols-2 gap-2 bg-metal-950 p-1 rounded-xl border border-metal-800">
            <button type="button" id="tabLocalFile" class="py-2 text-xs font-bold rounded-lg bg-rust-600 text-white transition">Local File</button>
            <button type="button" id="tabUrlFile" class="py-2 text-xs font-bold rounded-lg text-gray-400 hover:text-white transition">Video URL</button>
          </div>
        </div>

        <div id="fileInputContainer" class="border-2 border-dashed border-metal-700 hover:border-rust-500 rounded-xl p-6 text-center cursor-pointer bg-metal-950/50 hover:bg-metal-950 transition">
          <input type="file" id="videoFileInput" accept="video/mp4,video/webm,video/ogg" class="hidden">
          <i class="fa-solid fa-file-video text-3xl text-rust-500 mb-2"></i>
          <p id="fileSelectLabel" class="text-sm font-semibold text-gray-200">Click or drag & drop video file</p>
          <p class="text-xs text-gray-500 mt-1">MP4, WebM or OGG</p>
        </div>

        <div id="urlInputContainer" class="hidden space-y-2">
          <label class="block text-xs font-medium text-gray-300">Direct MP4 Video URL</label>
          <input type="url" id="videoUrlInput" placeholder="https://example.com/clip.mp4" 
                 class="w-full bg-metal-950 border border-metal-800 rounded-xl p-3 text-sm text-gray-200 focus:outline-none focus:border-rust-600">
        </div>

        <div>
          <label class="block text-xs font-semibold uppercase text-gray-400 mb-1">Title *</label>
          <input type="text" id="uploadTitle" required placeholder="Insane Clutch Highlight!" 
                 class="w-full bg-metal-950 border border-metal-800 rounded-xl p-3 text-sm text-gray-200 focus:outline-none focus:border-rust-600">
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-semibold uppercase text-gray-400 mb-1">Category</label>
            <select id="uploadCategory" class="w-full bg-metal-950 border border-metal-800 rounded-xl p-3 text-sm text-gray-200 focus:outline-none focus:border-rust-600">
              <option value="Gaming">Gaming</option>
              <option value="Fails">Fails & Fun</option>
              <option value="Highlights">Highlights</option>
              <option value="Retro">Retro Clips</option>
              <option value="Anime">Anime</option>
              <option value="Rusty Specials">Rusty Specials</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-semibold uppercase text-gray-400 mb-1">Creator Name</label>
            <input type="text" id="uploadAuthor" value="You (Rusty Creator)" 
                   class="w-full bg-metal-950 border border-metal-800 rounded-xl p-3 text-sm text-gray-200 focus:outline-none focus:border-rust-600">
          </div>
        </div>

        <div>
          <label class="block text-xs font-semibold uppercase text-gray-400 mb-1">Description</label>
          <textarea id="uploadDescription" rows="3" placeholder="Tell viewers about this epic moment..." 
                    class="w-full bg-metal-950 border border-metal-800 rounded-xl p-3 text-sm text-gray-200 focus:outline-none focus:border-rust-600 resize-none"></textarea>
        </div>

        <div id="uploadProgressContainer" class="hidden space-y-1.5">
          <div class="flex justify-between text-xs text-gray-400">
            <span id="uploadStatusText">Uploading & Processing...</span>
            <span id="uploadPercent">0%</span>
          </div>
          <div class="w-full bg-metal-950 rounded-full h-2.5 overflow-hidden border border-metal-800">
            <div id="uploadProgressBar" class="bg-gradient-to-r from-rust-600 to-amber-500 h-full w-0 transition-all duration-200"></div>
          </div>
        </div>

        <div class="flex justify-end gap-3 pt-2">
          <button type="button" id="cancelUploadBtn" class="px-4 py-2 text-xs font-semibold text-gray-400 hover:text-white transition">Cancel</button>
          <button type="submit" id="submitUploadBtn" class="bg-rust-600 hover:bg-rust-500 text-white text-xs font-bold px-6 py-2.5 rounded-xl transition shadow-lg rust-glow flex items-center gap-2">
            <i class="fa-solid fa-upload"></i> Publish Clip
          </button>
        </div>

      </form>
    </div>
  </div>

  <!-- TOAST NOTIFICATION -->
  <div id="toast" class="fixed bottom-5 right-5 z-50 bg-metal-900 border border-rust-500/50 text-white text-sm px-4 py-3 rounded-xl shadow-2xl flex items-center gap-3 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
    <div id="toastIcon" class="text-rust-500 text-lg">
      <i class="fa-solid fa-circle-check"></i>
    </div>
    <span id="toastMessage">Notification message</span>
  </div>

  <!-- SCRIPT CON PERSISTENCIA EN LOCALSTORAGE -->
  <script>
    const DEFAULT_VIDEOS = [
      {
        id: "clip-1",
        title: "Big Buck Bunny - Animated Short Film Classic",
        author: "Blender Animation Studio",
        avatar: "B",
        avatarBg: "bg-amber-700",
        views: "1.4M views",
        uploadedAt: "2 days ago",
        duration: "09:56",
        category: "Anime",
        videoUrl: "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4",
        thumbnailUrl: "https://images.unsplash.com/photo-1534447677768-be436bb09401?auto=format&fit=crop&w=800&q=80",
        description: "Big Buck Bunny tells the story of a giant rabbit with a heart bigger than himself.",
        likes: 45200,
        dislikes: 120,
        liked: false,
        saved: false,
        comments: []
      },
      {
        id: "clip-2",
        title: "Tears of Steel - Sci-Fi VFX Showcase",
        author: "Mango Open Movie Project",
        avatar: "M",
        avatarBg: "bg-rust-700",
        views: "890K views",
        uploadedAt: "1 week ago",
        duration: "12:14",
        category: "Highlights",
        videoUrl: "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/TearsOfSteel.mp4",
        thumbnailUrl: "https://images.unsplash.com/photo-1518709268805-4e9042af9f23?auto=format&fit=crop&w=800&q=80",
        description: "Set in a dystopian future in Amsterdam, a group of soldiers attempt to save the world.",
        likes: 31200,
        dislikes: 85,
        liked: false,
        saved: false,
        comments: []
      }
    ];

    const CATEGORIES = ["All", "Gaming", "Fails", "Highlights", "Retro", "Anime", "Rusty Specials"];

    // Cargar videos almacenados o inicializar por defecto
    let videos = JSON.parse(localStorage.getItem("kizaru_clips")) || DEFAULT_VIDEOS;
    let activeCategory = "All";
    let activeNav = "home";
    let currentVideoId = null;
    let selectedFile = null;

    function saveVideosToStorage() {
      localStorage.setItem("kizaru_clips", JSON.stringify(videos));
    }

    const feedView = document.getElementById('feedView');
    const watchView = document.getElementById('watchView');
    const videoGrid = document.getElementById('videoGrid');
    const emptyFeedState = document.getElementById('emptyFeedState');
    const categoryContainer = document.getElementById('categoryContainer');
    const searchInput = document.getElementById('searchInput');
    const feedTitle = document.getElementById('feedTitle');
    const videoCountBadge = document.getElementById('videoCountBadge');

    const mainVideoPlayer = document.getElementById('mainVideoPlayer');
    const playerTitle = document.getElementById('playerTitle');
    const playerAuthor = document.getElementById('playerAuthor');
    const playerAvatar = document.getElementById('playerAvatar');
    const playerViews = document.getElementById('playerViews');
    const playerDate = document.getElementById('playerDate');
    const playerCategoryBadge = document.getElementById('playerCategoryBadge');
    const playerDescription = document.getElementById('playerDescription');
    const likeBtn = document.getElementById('likeBtn');
    const dislikeBtn = document.getElementById('dislikeBtn');
    const likeCount = document.getElementById('likeCount');
    const dislikeCount = document.getElementById('dislikeCount');
    const saveBtn = document.getElementById('saveBtn');
    const saveIcon = document.getElementById('saveIcon');
    const saveText = document.getElementById('saveText');
    const subscribeBtn = document.getElementById('subscribeBtn');
    const recommendedContainer = document.getElementById('recommendedContainer');
    const commentsList = document.getElementById('commentsList');
    const commentInput = document.getElementById('commentInput');
    const submitCommentBtn = document.getElementById('submitCommentBtn');
    const cancelCommentBtn = document.getElementById('cancelCommentBtn');
    const commentsCountBadge = document.getElementById('commentsCountBadge');

    const uploadModal = document.getElementById('uploadModal');
    const openUploadModal = document.getElementById('openUploadModal');
    const closeUploadModal = document.getElementById('closeUploadModal');
    const cancelUploadBtn = document.getElementById('cancelUploadBtn');
    const uploadForm = document.getElementById('uploadForm');
    const tabLocalFile = document.getElementById('tabLocalFile');
    const tabUrlFile = document.getElementById('tabUrlFile');
    const fileInputContainer = document.getElementById('fileInputContainer');
    const urlInputContainer = document.getElementById('urlInputContainer');
    const videoFileInput = document.getElementById('videoFileInput');
    const videoUrlInput = document.getElementById('videoUrlInput');
    const fileSelectLabel = document.getElementById('fileSelectLabel');
    const uploadProgressContainer = document.getElementById('uploadProgressContainer');
    const uploadProgressBar = document.getElementById('uploadProgressBar');
    const uploadPercent = document.getElementById('uploadPercent');

    window.addEventListener('DOMContentLoaded', () => {
      renderCategories();
      renderFeed();
      setupEventListeners();
    });

    function renderCategories() {
      categoryContainer.innerHTML = CATEGORIES.map(cat => `
        <button data-cat="${cat}" class="category-btn text-xs font-semibold px-4 py-2 rounded-full whitespace-nowrap transition border ${
          cat === activeCategory 
            ? 'bg-rust-600 border-rust-500 text-white shadow-md' 
            : 'bg-metal-900 border-metal-800 text-gray-300 hover:bg-metal-800 hover:text-white'
        }">
          ${cat}
        </button>
      `).join('');

      document.querySelectorAll('.category-btn').forEach(btn => {
        btn.addEventListener('click', (e) => {
          activeCategory = e.currentTarget.dataset.cat;
          renderCategories();
          renderFeed();
        });
      });
    }

    function renderFeed() {
      const query = searchInput.value.trim().toLowerCase();

      let filtered = videos.filter(v => {
        if (activeNav === 'my-clips' && v.author !== 'You (Rusty Creator)') return false;
        if (activeNav === 'saved' && !v.saved) return false;
        if (activeCategory !== "All" && v.category !== activeCategory) return false;
        if (query) {
          return v.title.toLowerCase().includes(query) || v.description.toLowerCase().includes(query);
        }
        return true;
      });

      videoCountBadge.textContent = `${filtered.length} clips`;

      if (filtered.length === 0) {
        videoGrid.innerHTML = '';
        emptyFeedState.classList.remove('hidden');
        emptyFeedState.classList.add('flex');
        return;
      } else {
        emptyFeedState.classList.add('hidden');
        emptyFeedState.classList.remove('flex');
      }

      videoGrid.innerHTML = filtered.map(v => `
        <div data-id="${v.id}" class="video-card bg-metal-900 border border-metal-800/80 rounded-2xl overflow-hidden cursor-pointer hover:border-rust-600/60 transition group flex flex-col hover:shadow-xl">
          <div class="relative aspect-video bg-metal-950 overflow-hidden">
            <img src="${v.thumbnailUrl}" alt="${v.title}" class="w-full h-full object-cover group-hover:scale-105 transition duration-300" onerror="this.src='https://images.unsplash.com/photo-1518709268805-4e9042af9f23?auto=format&fit=crop&w=800&q=80'">
            <span class="absolute bottom-2 right-2 bg-black/80 text-white text-[11px] font-mono px-1.5 py-0.5 rounded">
              ${v.duration}
            </span>
            <div class="absolute inset-0 bg-black/30 opacity-0 group-hover:opacity-100 transition flex items-center justify-center">
              <div class="w-12 h-12 rounded-full bg-rust-600/90 text-white flex items-center justify-center pl-1 shadow-lg transform group-hover:scale-110 transition">
                <i class="fa-solid fa-play text-lg"></i>
              </div>
            </div>
          </div>
          <div class="p-3.5 flex gap-3 flex-1">
            <div class="w-8 h-8 rounded-full ${v.avatarBg || 'bg-rust-700'} flex-shrink-0 flex items-center justify-center text-xs font-bold text-white">
              ${v.avatar}
            </div>
            <div class="flex-1 min-w-0 flex flex-col justify-between">
              <div>
                <h3 class="text-sm font-semibold text-gray-100 group-hover:text-rust-400 transition line-clamp-2">
                  ${v.title}
                </h3>
                <p class="text-xs text-gray-400 mt-1 flex items-center gap-1">
                  <span>${v.author}</span>
                  <i class="fa-solid fa-circle-check text-[10px] text-rust-500"></i>
                </p>
              </div>
              <div class="text-[11px] text-gray-500 mt-2 flex items-center gap-2">
                <span>${v.views}</span>
                <span>•</span>
                <span>${v.uploadedAt}</span>
              </div>
            </div>
          </div>
        </div>
      `).join('');

      document.querySelectorAll('.video-card').forEach(card => {
        card.addEventListener('click', () => openVideoPlayer(card.dataset.id));
      });
    }

    function openVideoPlayer(videoId) {
      const video = videos.find(v => v.id === videoId);
      if (!video) return;

      currentVideoId = videoId;
      feedView.classList.add('hidden');
      watchView.classList.remove('hidden');

      mainVideoPlayer.src = video.videoUrl;
      mainVideoPlayer.poster = video.thumbnailUrl;
      mainVideoPlayer.play().catch(() => {});

      playerTitle.textContent = video.title;
      playerAuthor.textContent = video.author;
      playerAvatar.textContent = video.avatar;
      playerViews.textContent = video.views;
      playerDate.textContent = video.uploadedAt;
      playerCategoryBadge.textContent = video.category;
      playerDescription.textContent = video.description || "No description.";

      likeCount.textContent = video.likes;
      dislikeCount.textContent = video.dislikes;

      updateSaveBtnUI(video.saved);
      renderComments(video);
      renderRecommended(video.id);
    }

    function renderRecommended(currentId) {
      const recs = videos.filter(v => v.id !== currentId);
      recommendedContainer.innerHTML = recs.map(v => `
        <div data-id="${v.id}" class="rec-card flex gap-3 p-2 rounded-xl bg-metal-900/60 hover:bg-metal-900 border border-metal-800/50 hover:border-rust-600/50 transition cursor-pointer group">
          <div class="relative w-36 aspect-video bg-black rounded-lg overflow-hidden flex-shrink-0">
            <img src="${v.thumbnailUrl}" class="w-full h-full object-cover group-hover:scale-105 transition" onerror="this.src='https://images.unsplash.com/photo-1518709268805-4e9042af9f23?auto=format&fit=crop&w=800&q=80'">
          </div>
          <div class="flex-1 min-w-0 flex flex-col justify-between">
            <h4 class="text-xs font-semibold text-gray-200 group-hover:text-rust-400 transition line-clamp-2">
              ${v.title}
            </h4>
            <p class="text-[11px] text-gray-400">${v.author}</p>
          </div>
        </div>
      `).join('');

      document.querySelectorAll('.rec-card').forEach(card => {
        card.addEventListener('click', () => openVideoPlayer(card.dataset.id));
      });
    }

    function renderComments(video) {
      const comments = video.comments || [];
      commentsCountBadge.textContent = comments.length;
      commentsList.innerHTML = comments.map(c => `
        <div class="flex gap-3 text-sm border-b border-metal-800/50 pb-3">
          <div class="w-8 h-8 rounded-full bg-rust-700 flex items-center justify-center font-bold text-xs text-white">
            ${c.avatar}
          </div>
          <div>
            <div class="flex items-center gap-2">
              <span class="font-bold text-xs text-gray-200">${c.author}</span>
              <span class="text-[10px] text-gray-500">${c.date}</span>
            </div>
            <p class="text-xs text-gray-300">${c.text}</p>
          </div>
        </div>
      `).join('');
    }

    function setupEventListeners() {
      document.querySelectorAll('.nav-item').forEach(item => {
        item.addEventListener('click', (e) => {
          activeNav = e.currentTarget.dataset.nav;
          watchView.classList.add('hidden');
          feedView.classList.remove('hidden');
          renderFeed();
        });
      });

      document.getElementById('brandLogo').addEventListener('click', (e) => {
        e.preventDefault();
        watchView.classList.add('hidden');
        feedView.classList.remove('hidden');
        renderFeed();
      });

      likeBtn.addEventListener('click', () => {
        const video = videos.find(v => v.id === currentVideoId);
        if (!video) return;
        video.likes++;
        likeCount.textContent = video.likes;
        saveVideosToStorage();
        showToast('Liked clip!');
      });

      saveBtn.addEventListener('click', () => {
        const video = videos.find(v => v.id === currentVideoId);
        if (!video) return;
        video.saved = !video.saved;
        updateSaveBtnUI(video.saved);
        saveVideosToStorage();
        showToast(video.saved ? 'Saved clip!' : 'Removed from saved');
      });

      submitCommentBtn.addEventListener('click', () => {
        const text = commentInput.value.trim();
        if (!text) return;
        const video = videos.find(v => v.id === currentVideoId);
        if (!video) return;

        if (!video.comments) video.comments = [];
        video.comments.unshift({
          id: 'c-' + Date.now(),
          author: 'You (Rusty Creator)',
          avatar: 'Y',
          text: text,
          date: 'Just now'
        });

        commentInput.value = '';
        saveVideosToStorage();
        renderComments(video);
        showToast('Comment added!');
      });

      openUploadModal.addEventListener('click', () => {
        uploadModal.classList.remove('hidden');
        setTimeout(() => uploadModal.classList.remove('opacity-0'), 10);
      });

      closeUploadModal.addEventListener('click', () => {
        uploadModal.classList.add('opacity-0');
        setTimeout(() => uploadModal.classList.add('hidden'), 200);
      });

      videoFileInput.addEventListener('change', (e) => {
        if (e.target.files.length > 0) {
          selectedFile = e.target.files[0];
          fileSelectLabel.textContent = selectedFile.name;
        }
      });

      uploadForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const title = document.getElementById('uploadTitle').value.trim();
        const category = document.getElementById('uploadCategory').value;
        const author = document.getElementById('uploadAuthor').value.trim() || 'Anonymous';
        const description = document.getElementById('uploadDescription').value.trim();
        
        let videoUrl = videoUrlInput.value.trim();
        if (selectedFile) {
          videoUrl = URL.createObjectURL(selectedFile);
        }

        const newClip = {
          id: 'clip-' + Date.now(),
          title: title,
          author: author,
          avatar: author.charAt(0).toUpperCase(),
          avatarBg: 'bg-rust-600',
          views: '1 view',
          uploadedAt: 'Just now',
          duration: '00:30',
          category: category,
          videoUrl: videoUrl || 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4',
          thumbnailUrl: 'https://images.unsplash.com/photo-1542751371-adc38448a05e?auto=format&fit=crop&w=800&q=80',
          description: description,
          likes: 0,
          dislikes: 0,
          saved: false,
          comments: []
        };

        videos.unshift(newClip);
        saveVideosToStorage();

        uploadModal.classList.add('opacity-0');
        setTimeout(() => uploadModal.classList.add('hidden'), 200);
        showToast('Video uploaded successfully!');
        renderFeed();
      });
    }

    function updateSaveBtnUI(isSaved) {
      if (isSaved) {
        saveIcon.classList.add('fa-solid', 'text-rust-500');
        saveText.textContent = 'Saved';
      } else {
        saveIcon.classList.remove('fa-solid', 'text-rust-500');
        saveText.textContent = 'Save';
      }
    }

    function showToast(message) {
      const toast = document.getElementById('toast');
      document.getElementById('toastMessage').textContent = message;
      toast.classList.remove('translate-y-20', 'opacity-0');
      setTimeout(() => toast.classList.add('translate-y-20', 'opacity-0'), 3000);
    }
  </script>
</body>
</html>