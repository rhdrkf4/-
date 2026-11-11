[index.html](https://github.com/user-attachments/files/34681204/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>플레이어 라운지 | 게임 커뮤니티</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            brand: {
              50: '#f0f7ff',
              100: '#e0effe',
              500: '#3b82f6',
              600: '#2563eb',
              700: '#1d4ed8',
            }
          }
        }
      }
    }
  </script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Pretendard:wght@300;400;500;600;700;800&display=swap');
    body.bg-slate-50 {
      background-color: #f2f6f4;
      background-image:
        radial-gradient(ellipse at 8% 0%, rgba(52, 126, 117, 0.08), transparent 34rem),
        radial-gradient(ellipse at 96% 12%, rgba(225, 168, 84, 0.08), transparent 30rem);
      font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, system-ui, Roboto, sans-serif;
    }
    header.sticky {
      box-shadow: 0 1px 0 rgba(22, 42, 44, 0.06), 0 8px 24px rgba(22, 42, 44, 0.035);
    }
    .game-discovery {
      position: relative;
      overflow: visible;
      padding: 1.25rem;
      color: #f4f8f6;
      background-color: #17343a;
      background-image: radial-gradient(rgba(220, 239, 230, 0.1) 1px, transparent 1px);
      background-size: 18px 18px;
      border: 1px solid rgba(25, 58, 61, 0.8);
      border-radius: 12px;
      box-shadow: 0 10px 24px rgba(22, 42, 44, 0.08);
    }
    .game-discovery h2 { color: #fff; }
    .game-discovery p { color: #c8d8d5; }
    #gameSearchInput { min-height: 44px; }
    #gameSearchInput:focus {
      border-color: #8bc9b7;
      box-shadow: 0 0 0 3px rgba(139, 201, 183, 0.22);
    }
    #gameSearchSubmit {
      background-color: #d3a64e;
      color: #202a27;
    }
    #gameSearchSubmit:hover { background-color: #e2b65f; }
    #popularGameButtons button {
      border-color: rgba(232, 241, 235, 0.2);
      background: rgba(255, 255, 255, 0.08);
      color: #f1f5f2;
    }
    #popularGameButtons button:hover {
      border-color: #d3a64e;
      background: rgba(255, 255, 255, 0.14);
      color: #fff;
    }
    #popularGameButtons button span { color: #c8d8d5; }
    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: #f1f5f9;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 4px;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb:hover {
      background: #94a3b8;
    }
  </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col antialiased selection:bg-blue-100 selection:text-blue-700">

  <!-- ==================== 네비게이션 헤더 ==================== -->
  <header class="sticky top-0 z-40 bg-white/95 backdrop-blur border-b border-slate-200 shadow-xs">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 h-16 flex items-center justify-between gap-4">
      <!-- 로고 -->
      <a href="javascript:void(0)" onclick="app.navigateToList('all')" class="flex items-center gap-2.5 group">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-blue-600 to-indigo-600 flex items-center justify-center text-white shadow-md shadow-blue-500/20 group-hover:scale-105 transition-transform">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 20H5a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2v1m2 13a2 2 0 01-2-2V7m2 13a2 2 0 002-2V9a2 2 0 00-2-2h-2m-4-3H9M7 16h6M7 8h6v4H7V8z"/>
          </svg>
        </div>
        <div class="flex flex-col">
          <span class="whitespace-nowrap font-bold text-lg leading-tight text-slate-900 group-hover:text-blue-600 transition-colors">플레이어 라운지</span>
          <span class="text-xs text-slate-500 font-medium">게임 커뮤니티</span>
        </div>
      </a>

      <!-- 우측 사용자 인증 바 -->
      <div id="authNavContainer" class="flex items-center gap-3">
        <!-- JS로 동적 렌더링 -->
      </div>
    </div>
  </header>

  <!-- ==================== 메인 컨텐츠 영역 ==================== -->
  <main class="max-w-6xl mx-auto px-4 sm:px-6 py-6 w-full flex-1">
    
    <!-- 1. 게시판 탭 바 & 검색 바 (목록 화면에서 표시) -->
    <div id="boardHeaderSection" class="mb-6 space-y-4">
      <!-- 상단 탭 메뉴 -->
      <div class="flex items-center justify-between border-b border-slate-200 overflow-x-auto custom-scrollbar pb-1">
        <nav class="flex gap-2 sm:gap-4 shrink-0" id="boardTabsNav">
          <!-- JS로 동적 생성 -->
        </nav>
        <button onclick="app.openEditor()" class="hidden md:inline-flex items-center gap-1.5 px-4 py-2 bg-blue-600 hover:bg-blue-700 active:scale-95 text-white text-sm font-semibold rounded-lg shadow-sm shadow-blue-500/30 transition-all">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
          </svg>
          새 글 작성
        </button>
      </div>

      <section id="gameSearchSection" class="game-discovery space-y-3">
        <div class="flex flex-col lg:flex-row lg:items-end justify-between gap-3">
          <div>
            <h2 class="text-lg font-bold">어떤 게임 이야기를 찾고 있나요?</h2>
            <p class="text-xs mt-1">모바일과 PC 게임을 검색해 플레이어의 대화와 공략을 둘러보세요.</p>
          </div>
          <div class="relative w-full sm:max-w-md">
            <div class="flex gap-2">
              <input id="gameSearchInput" type="search" autocomplete="off" placeholder="예: 원신, 마인크래프트, 발로란트"
                     oninput="app.searchGames(this.value)"
                     onkeydown="if(event.key==='Enter'){event.preventDefault();app.applyGameSearch();}"
                     class="min-w-0 flex-1 px-3.5 py-2.5 text-sm bg-white border border-slate-300 rounded-lg focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 shadow-xs">
              <button id="gameSearchSubmit" onclick="app.applyGameSearch()" class="px-4 py-2.5 text-sm font-bold rounded-lg transition">게임 검색</button>
            </div>
            <div id="gameSearchResults" class="hidden absolute z-30 top-full mt-1 w-full bg-white border border-slate-200 rounded-lg shadow-lg overflow-hidden"></div>
          </div>
        </div>
        <div id="popularGameButtons" class="flex gap-2 overflow-x-auto custom-scrollbar pb-1"></div>
      </section>

      <!-- 보조 툴바: 게시판 설명 & 정렬 및 검색 -->
      <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 pt-2">
        <div>
          <h1 id="currentBoardTitle" class="text-xl font-bold text-slate-900 flex items-center gap-2">
            전체 게시글
          </h1>
          <p id="currentBoardDesc" class="text-xs text-slate-500 mt-0.5">
            등록된 모든 게시글을 최신순으로 확인하세요.
          </p>
        </div>

        <div class="flex items-center gap-2">
          <!-- 검색창 -->
          <div class="relative w-full sm:w-64">
            <input type="text" id="searchInput" placeholder="제목, 내용, 작성자 검색..."
                   onkeyup="if(event.key==='Enter') app.handleSearch()"
                   class="w-full pl-9 pr-8 py-2 text-sm bg-white border border-slate-300 rounded-lg focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition-all shadow-xs">
            <svg class="w-4 h-4 text-slate-400 absolute left-3 top-2.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
            </svg>
            <button id="clearSearchBtn" onclick="app.clearSearch()" class="hidden absolute right-2.5 top-2.5 text-slate-400 hover:text-slate-600">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
              </svg>
            </button>
          </div>

          <!-- 정렬 셀렉트 -->
          <select id="sortSelect" onchange="app.handleSortChange(this.value)"
                  class="bg-white border border-slate-300 text-slate-700 text-sm rounded-lg px-3 py-2 focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition shadow-xs">
            <option value="newest">최신순</option>
            <option value="views">조회수순</option>
            <option value="comments">댓글 많은순</option>
          </select>

          <!-- 모바일용 글쓰기 버튼 -->
          <button onclick="app.openEditor()" class="md:hidden inline-flex items-center justify-center p-2 bg-blue-600 text-white rounded-lg shadow-sm">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- ==================== 뷰 1: 게시글 목록 (List View) ==================== -->
    <div id="listView" class="space-y-4">
      <div class="bg-white rounded-xl border border-slate-200 shadow-xs overflow-hidden">
        <div id="postListContainer" class="divide-y divide-slate-100">
          <!-- JS로 동적 게시글 리스트 렌더링 -->
        </div>
      </div>

      <!-- 페이지네이션 컨트롤 -->
      <div id="paginationContainer" class="flex items-center justify-center gap-1.5 py-4">
        <!-- JS로 동적 페이지 버튼 생성 -->
      </div>
    </div>

    <!-- ==================== 뷰 2: 게시글 상세 (Detail View) ==================== -->
    <div id="detailView" class="hidden space-y-6">
      <!-- 상단 액션 바 -->
      <div class="flex items-center justify-between">
        <button onclick="app.backToList()" class="inline-flex items-center gap-1 text-sm font-medium text-slate-600 hover:text-slate-900 transition-colors">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18"/>
          </svg>
          게시판 목록으로 돌아가기
        </button>

        <!-- 작성자 권한 컨트롤 (본인인 경우에만 표시) -->
        <div id="authorActionButtons" class="hidden items-center gap-2">
          <button onclick="app.openEditorForEdit()" class="inline-flex items-center gap-1 px-3 py-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold rounded-lg transition">
            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z"/>
            </svg>
            수정
          </button>
          <button onclick="app.confirmDeletePost()" class="inline-flex items-center gap-1 px-3 py-1.5 bg-rose-50 hover:bg-rose-100 text-rose-600 text-xs font-semibold rounded-lg transition">
            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
            </svg>
            삭제
          </button>
        </div>
      </div>

      <!-- 본문 카드 -->
      <article class="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 sm:p-8 space-y-6">
        <!-- 헤더 정보 -->
        <div class="border-b border-slate-100 pb-5 space-y-3">
          <div class="flex items-center gap-2">
            <span id="detailBoardBadge" class="px-2.5 py-0.5 text-xs font-semibold rounded-md"></span>
            <span id="detailGameBadge" class="hidden px-2.5 py-0.5 text-xs font-semibold rounded-md bg-blue-50 text-blue-700 border border-blue-100"></span>
            <span id="detailDate" class="text-xs text-slate-400"></span>
          </div>
          <h1 id="detailTitle" class="text-2xl sm:text-3xl font-bold text-slate-900 leading-snug break-words"></h1>
          
          <div class="flex items-center justify-between text-xs text-slate-500 pt-2">
            <div class="flex items-center gap-2.5">
              <div id="detailAuthorAvatar" class="w-8 h-8 rounded-full bg-blue-100 text-blue-700 flex items-center justify-center font-bold text-sm"></div>
              <div>
                <p id="detailAuthorName" class="font-semibold text-slate-800 text-sm"></p>
                <p id="detailAuthorSub" class="text-slate-400 text-[11px]"></p>
              </div>
            </div>
            <div class="flex items-center gap-3">
              <span class="flex items-center gap-1" title="조회수">
                <svg class="w-4 h-4 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"/>
                </svg>
                <span id="detailViews">0</span>
              </span>
              <span class="flex items-center gap-1" title="댓글수">
                <svg class="w-4 h-4 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"/>
                </svg>
                <span id="detailCommentsCount">0</span>
              </span>
            </div>
          </div>
        </div>

        <!-- 본문 텍스트 -->
        <div id="detailContent" class="text-slate-700 leading-relaxed text-base sm:text-lg min-h-[160px] whitespace-pre-wrap break-words"></div>
      </article>

      <!-- 댓글 영역 -->
      <section class="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 sm:p-8 space-y-6">
        <div class="flex items-center justify-between border-b border-slate-100 pb-4">
          <h2 class="text-lg font-bold text-slate-900 flex items-center gap-2">
            <span>댓글</span>
            <span id="commentSectionCount" class="text-blue-600 bg-blue-50 text-xs px-2 py-0.5 rounded-full font-semibold">0</span>
          </h2>
        </div>

        <!-- 댓글 입력 폼 -->
        <div id="commentFormWrapper" class="space-y-2">
          <!-- 비로그인시 가이드 or 로그인시 입력창 렌더링 -->
        </div>

        <!-- 댓글 목록 -->
        <div id="commentListContainer" class="space-y-4 pt-2">
          <!-- 동적 렌더링 -->
        </div>
      </section>
    </div>

    <!-- ==================== 뷰 3: 글 작성 및 수정 (Editor View) ==================== -->
    <div id="editorView" class="hidden space-y-6">
      <div class="flex items-center justify-between">
        <h1 id="editorPageTitle" class="text-2xl font-bold text-slate-900">새 게시글 작성</h1>
        <button onclick="app.cancelEditor()" class="text-sm text-slate-500 hover:text-slate-800 transition">취소하고 돌아가기</button>
      </div>

      <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 sm:p-8 space-y-5">
        <form id="postForm" onsubmit="app.handleSavePost(event)" class="space-y-5">
          <input type="hidden" id="editPostId" value="">

          <!-- 게시판 선택 -->
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1.5">게시판 선택 <span class="text-rose-500">*</span></label>
            <select id="formBoardSelect" required class="w-full sm:w-64 px-3.5 py-2.5 text-sm bg-white border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition shadow-xs font-medium">
              <!-- JS로 옵션 로드 -->
            </select>
          </div>

          <div>
            <label for="formGameInput" class="block text-xs font-semibold text-slate-600 mb-1.5">게임 <span class="text-slate-400 font-normal">선택 사항</span></label>
            <input id="formGameInput" type="text" list="gameCatalogOptions" maxlength="50" autocomplete="off" placeholder="게임을 검색하거나 이름을 직접 입력하세요"
                   class="w-full sm:w-96 px-3.5 py-2.5 text-sm bg-white border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition shadow-xs">
            <datalist id="gameCatalogOptions"></datalist>
          </div>

          <!-- 제목 -->
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1.5">제목 <span class="text-rose-500">*</span></label>
            <input type="text" id="formTitleInput" required placeholder="게시글 제목을 입력해주세요" maxlength="120"
                   class="w-full px-4 py-2.5 text-base bg-white border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition shadow-xs">
          </div>

          <!-- 본문 -->
          <div>
            <div class="flex items-center justify-between mb-1.5">
              <label class="block text-xs font-semibold text-slate-600">내용 <span class="text-rose-500">*</span></label>
              <span class="text-xs text-slate-400" id="contentLengthHint">0 / 5,000자</span>
            </div>
            <textarea id="formContentInput" required rows="12" placeholder="자유롭게 이야기를 작성해보세요. 줄바꿈과 서식이 유지됩니다."
                      oninput="document.getElementById('contentLengthHint').innerText = this.value.length.toLocaleString() + ' / 5,000자'"
                      class="w-full px-4 py-3 text-sm sm:text-base bg-white border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition shadow-xs leading-relaxed resize-y custom-scrollbar"></textarea>
          </div>

          <!-- 하단 버튼 -->
          <div class="flex items-center justify-end gap-3 pt-4 border-t border-slate-100">
            <button type="button" onclick="app.cancelEditor()" class="px-5 py-2.5 rounded-xl border border-slate-300 text-slate-700 text-sm font-semibold hover:bg-slate-50 transition">
              취소
            </button>
            <button type="submit" id="submitPostBtn" class="px-6 py-2.5 rounded-xl bg-blue-600 hover:bg-blue-700 active:scale-95 text-white text-sm font-semibold shadow-sm shadow-blue-500/30 transition-all">
              게시글 등록
            </button>
          </div>
        </form>
      </div>
    </div>

  </main>

  <!-- ==================== 푸터 ==================== -->
  <footer class="mt-auto border-t border-slate-200 bg-white py-6 text-center text-xs text-slate-400">
    <div class="max-w-6xl mx-auto px-4">
      <p>© 2026 플레이어 라운지. 게임 이야기를 나누는 커뮤니티.</p>
      <p class="mt-1">공지사항 · 자유게시판 · 게임 Q&A · 공략·팁</p>
    </div>
  </footer>

  <!-- ==================== 로그인 모달 ==================== -->
  <div id="loginModal" class="hidden fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/50 backdrop-blur-xs">
    <div class="bg-white rounded-2xl max-w-sm w-full p-6 sm:p-7 shadow-2xl border border-slate-100 space-y-5 animate-in fade-in duration-200">
      <div class="flex items-center justify-between">
        <div>
          <h2 class="text-xl font-bold text-slate-900">로그인</h2>
          <p class="text-xs text-slate-500 mt-0.5">게시판 활동을 시작하세요.</p>
        </div>
        <button onclick="app.closeModal('loginModal')" class="text-slate-400 hover:text-slate-600 p-1">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
          </svg>
        </button>
      </div>

      <!-- 테스트 계정 퀵 버튼 -->
      <div class="bg-blue-50 border border-blue-100 rounded-xl p-3 text-xs space-y-1.5">
        <p class="font-bold text-blue-800 flex items-center gap-1">
          <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
          </svg>
          빠른 테스트 로그인:
        </p>
        <div class="grid grid-cols-3 gap-1.5 pt-1">
          <button onclick="app.quickLogin('admin')" class="py-1 px-2 bg-white hover:bg-blue-100 border border-blue-200 rounded text-blue-700 font-medium transition text-center">운영자</button>
          <button onclick="app.quickLogin('chulsoo')" class="py-1 px-2 bg-white hover:bg-blue-100 border border-blue-200 rounded text-blue-700 font-medium transition text-center">김철수</button>
          <button onclick="app.quickLogin('younghee')" class="py-1 px-2 bg-white hover:bg-blue-100 border border-blue-200 rounded text-blue-700 font-medium transition text-center">이영희</button>
        </div>
      </div>

      <form onsubmit="app.handleLogin(event)" class="space-y-3.5">
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">아이디</label>
          <input type="text" id="loginUsername" required placeholder="아이디를 입력하세요"
                 class="w-full px-3.5 py-2 text-sm border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">비밀번호</label>
          <input type="password" id="loginPassword" required placeholder="비밀번호를 입력하세요"
                 class="w-full px-3.5 py-2 text-sm border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition">
        </div>
        <button type="submit" class="w-full py-2.5 bg-blue-600 hover:bg-blue-700 text-white rounded-xl font-semibold text-sm shadow-sm transition">
          로그인
        </button>
      </form>

      <div class="text-center pt-2 border-t border-slate-100 text-xs text-slate-500">
        아직 회원이 아니신가요? 
        <button onclick="app.switchModal('loginModal', 'registerModal')" class="text-blue-600 font-bold hover:underline ml-1">회원가입</button>
      </div>
    </div>
  </div>

  <!-- ==================== 회원가입 모달 ==================== -->
  <div id="registerModal" class="hidden fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/50 backdrop-blur-xs">
    <div class="bg-white rounded-2xl max-w-sm w-full p-6 sm:p-7 shadow-2xl border border-slate-100 space-y-5 animate-in fade-in duration-200">
      <div class="flex items-center justify-between">
        <div>
          <h2 class="text-xl font-bold text-slate-900">회원가입</h2>
          <p class="text-xs text-slate-500 mt-0.5">새로운 계정을 생성하세요.</p>
        </div>
        <button onclick="app.closeModal('registerModal')" class="text-slate-400 hover:text-slate-600 p-1">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
          </svg>
        </button>
      </div>

      <form onsubmit="app.handleRegister(event)" class="space-y-3.5">
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">아이디</label>
          <input type="text" id="regUsername" required placeholder="영문, 숫자 4자 이상" minlength="3" maxlength="20"
                 class="w-full px-3.5 py-2 text-sm border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">닉네임</label>
          <input type="text" id="regNickname" required placeholder="활동할 닉네임 (2자 이상)" minlength="2" maxlength="15"
                 class="w-full px-3.5 py-2 text-sm border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">비밀번호</label>
          <input type="password" id="regPassword" required placeholder="4자 이상 입력" minlength="4"
                 class="w-full px-3.5 py-2 text-sm border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">비밀번호 확인</label>
          <input type="password" id="regPasswordConfirm" required placeholder="비밀번호 재입력"
                 class="w-full px-3.5 py-2 text-sm border border-slate-300 rounded-xl focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition">
        </div>
        <button type="submit" class="w-full py-2.5 bg-blue-600 hover:bg-blue-700 text-white rounded-xl font-semibold text-sm shadow-sm transition">
          가입하기
        </button>
      </form>

      <div class="text-center pt-2 border-t border-slate-100 text-xs text-slate-500">
        이미 계정이 있으신가요? 
        <button onclick="app.switchModal('registerModal', 'loginModal')" class="text-blue-600 font-bold hover:underline ml-1">로그인</button>
      </div>
    </div>
  </div>

  <!-- ==================== 확인 모달 (Confirm Modal) ==================== -->
  <div id="confirmModal" class="hidden fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/50 backdrop-blur-xs">
    <div class="bg-white rounded-2xl max-w-sm w-full p-6 shadow-2xl border border-slate-100 space-y-4">
      <div class="w-12 h-12 rounded-full bg-rose-100 text-rose-600 flex items-center justify-center mx-auto">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/>
        </svg>
      </div>
      <div class="text-center space-y-1">
        <h3 id="confirmModalTitle" class="text-lg font-bold text-slate-900">확인</h3>
        <p id="confirmModalMessage" class="text-xs text-slate-500">정말 진행하시겠습니까?</p>
      </div>
      <div class="grid grid-cols-2 gap-2 pt-2">
        <button onclick="app.closeModal('confirmModal')" class="py-2 px-3 border border-slate-300 text-slate-700 text-sm font-semibold rounded-xl hover:bg-slate-50 transition">
          취소
        </button>
        <button id="confirmModalBtn" class="py-2 px-3 bg-rose-600 hover:bg-rose-700 text-white text-sm font-semibold rounded-xl transition">
          삭제하기
        </button>
      </div>
    </div>
  </div>

  <!-- ==================== 알림 토스트 (Toast Container) ==================== -->
  <div id="toastContainer" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 max-w-sm w-full pointer-events-none"></div>

  <!-- ==================== 핵심 자바스크립트 로직 ==================== -->
  <script>
    /**
     * 모두의 다중 게시판 단일 앱 (SPA)
     */
    const BOARDS = [
      { id: 'all', name: '전체글', icon: '📋', desc: '모든 게시판의 글을 한눈에 모아봅니다.', color: 'bg-slate-100 text-slate-700 border-slate-200' },
      { id: 'notice', name: '공지사항', icon: '📢', desc: '커뮤니티 소식과 함께 알아둘 게임 소식을 확인하세요.', color: 'bg-rose-50 text-rose-700 border-rose-200' },
      { id: 'free', name: '자유게시판', icon: '🎮', desc: '요즘 하는 게임과 플레이 경험을 자유롭게 나눠보세요.', color: 'bg-blue-50 text-blue-700 border-blue-200' },
      { id: 'qna', name: '게임 Q&A', icon: '❓', desc: '게임 관련 질문을 올리고 다른 플레이어의 답변을 받아보세요.', color: 'bg-amber-50 text-amber-700 border-amber-200' },
      { id: 'info', name: '공략·팁', icon: '🧭', desc: '공략, 빌드, 숨겨진 요소와 유용한 플레이 팁을 공유하세요.', color: 'bg-emerald-50 text-emerald-700 border-emerald-200' }
    ];

    const GAME_CATALOG = [
      { name: '마인크래프트', platform: 'PC · 모바일', keywords: 'minecraft 샌드박스 생존 건축' },
      { name: '발로란트', platform: 'PC', keywords: 'valorant FPS 슈팅' },
      { name: '리그 오브 레전드', platform: 'PC', keywords: 'league of legends lol 롤 MOBA' },
      { name: '원신', platform: 'PC · 모바일', keywords: 'genshin impact 오픈월드 RPG' },
      { name: '로블록스', platform: 'PC · 모바일', keywords: 'roblox 샌드박스' },
      { name: '배틀그라운드 모바일', platform: '모바일', keywords: 'pubg mobile 배그' },
      { name: '배틀그라운드', platform: 'PC', keywords: 'pubg 배그' },
      { name: '붕괴: 스타레일', platform: 'PC · 모바일', keywords: 'honkai star rail RPG' },
      { name: '포켓몬 GO', platform: '모바일', keywords: 'pokemon go 포켓몬고 AR' },
      { name: '메이플스토리', platform: 'PC', keywords: 'maplestory MMORPG' },
      { name: '메이플스토리M', platform: '모바일', keywords: 'maplestory m 메이플M' },
      { name: 'FC 모바일', platform: '모바일', keywords: 'fc mobile 축구' },
      { name: '오버워치 2', platform: 'PC', keywords: 'overwatch 2 FPS' },
      { name: '로스트아크', platform: 'PC', keywords: 'lost ark MMORPG' },
      { name: '스타듀 밸리', platform: 'PC · 모바일', keywords: 'stardew valley 농장' },
      { name: '쿠키런: 킹덤', platform: '모바일', keywords: 'cookie run kingdom RPG' },
      { name: '명조: 워더링 웨이브', platform: 'PC · 모바일', keywords: 'wuthering waves RPG' },
      { name: '클래시 로얄', platform: '모바일', keywords: 'clash royale 전략' },
      { name: '이터널 리턴', platform: 'PC', keywords: 'eternal return 생존' },
      { name: '디아블로 IV', platform: 'PC', keywords: 'diablo 4 액션 RPG' }
    ];

    const STORAGE_KEYS = {
      USERS: 'multiboard_v1_users',
      POSTS: 'multiboard_v1_posts',
      COMMENTS: 'multiboard_v1_comments',
      SESSION: 'multiboard_v1_session'
    };

    // 초기 데모 데이터 시딩
    function seedInitialData() {
      if (!localStorage.getItem(STORAGE_KEYS.USERS)) {
        const defaultUsers = [
          { id: 'u_admin', username: 'admin', password: 'admin123', nickname: '운영자', role: 'admin', createdAt: '2026-11-01 10:00:00' },
          { id: 'u_chulsoo', username: 'chulsoo', password: '1234', nickname: '김철수', role: 'user', createdAt: '2026-11-02 11:30:00' },
          { id: 'u_younghee', username: 'younghee', password: '1234', nickname: '이영희', role: 'user', createdAt: '2026-11-03 14:15:00' }
        ];
        localStorage.setItem(STORAGE_KEYS.USERS, JSON.stringify(defaultUsers));
      }

      if (!localStorage.getItem(STORAGE_KEYS.POSTS)) {
        const defaultPosts = [
          {
            id: 'p_1',
            boardId: 'notice',
            title: '🎮 플레이어 라운지에 오신 것을 환영합니다!',
            content: `안녕하세요! 게임을 좋아하는 플레이어들이 모여 이야기 나누는 공간입니다.\n\n게임 소식은 공지사항에서, 플레이 경험은 자유게시판에서 나눠보세요. 막히는 부분은 게임 Q&A에 질문하고, 도움이 된 공략과 팁은 다른 플레이어들과 공유할 수 있습니다.\n\n좋아하는 게임이 달라도 서로 존중하며 즐겁게 소통해요!`,
            authorId: 'u_admin',
            authorNickname: '운영자',
            views: 124,
            createdAt: '2026-11-10 09:30:00',
            updatedAt: '2026-11-10 09:30:00'
          },
          {
            id: 'p_2',
            boardId: 'free',
            gameName: '마인크래프트',
            title: '마인크래프트 생존 모드, 첫날에 뭐부터 하세요?',
            content: '새 월드에서 생존을 시작하면 첫날에 무엇부터 준비하시나요?\n저는 나무와 돌 도구를 먼저 모으고 밤이 오기 전에 간단한 집을 만들어요. 초반 생존에 유용한 팁이 있다면 알려주세요!',
            authorId: 'u_chulsoo',
            authorNickname: '김철수',
            views: 45,
            createdAt: '2026-11-11 11:10:00',
            updatedAt: '2026-11-11 11:10:00'
          },
          {
            id: 'p_3',
            boardId: 'qna',
            title: '친구들과 가볍게 즐길 협동 게임을 추천해주세요',
            content: '주말에 친구들과 같이 할 협동 게임을 찾고 있습니다.\n인원은 3~4명이고, 처음 하는 사람도 쉽게 적응할 수 있는 게임이면 좋겠어요. 직접 해본 게임 중 재미있었던 작품과 추천 이유를 알려주세요!',
            authorId: 'u_younghee',
            authorNickname: '이영희',
            views: 32,
            createdAt: '2026-11-11 12:05:00',
            updatedAt: '2026-11-11 12:05:00'
          },
          {
            id: 'p_4',
            boardId: 'info',
            title: '처음 만난 파티와도 편하게 소통하는 방법',
            content: '온라인 파티에서는 짧고 분명한 콜아웃이 큰 도움이 됩니다.\n\n- 필요한 정보부터 간결하게 전달하기\n- 실수했을 때 탓하기보다 다음 행동을 함께 정하기\n- 음성 채팅이 부담스럽다면 게임 내 핑과 채팅 활용하기\n- 팀원마다 플레이 방식이 다를 수 있다는 점 존중하기\n\n즐거운 플레이는 좋은 소통에서 시작됩니다!',
            authorId: 'u_admin',
            authorNickname: '운영자',
            views: 89,
            createdAt: '2026-11-11 12:45:00',
            updatedAt: '2026-11-11 12:45:00'
          }
        ];
        localStorage.setItem(STORAGE_KEYS.POSTS, JSON.stringify(defaultPosts));
      }

      if (!localStorage.getItem(STORAGE_KEYS.COMMENTS)) {
        const defaultComments = [
          {
            id: 'c_1',
            postId: 'p_1',
            authorId: 'u_chulsoo',
            authorNickname: '김철수',
            content: '게임 좋아하는 사람들과 편하게 이야기 나눌 수 있어서 좋네요. 자주 올게요!',
            createdAt: '2026-11-10 10:15:00'
          },
          {
            id: 'c_2',
            postId: 'p_2',
            authorId: 'u_younghee',
            authorNickname: '이영희',
            content: '저는 요즘 친구들이랑 하는 협동 게임에 푹 빠졌어요. 같이 하면 더 재미있더라고요!',
            createdAt: '2026-11-11 11:20:00'
          },
          {
            id: 'c_3',
            postId: 'p_3',
            authorId: 'u_admin',
            authorNickname: '운영자',
            content: '처음 시작할 때는 튜토리얼과 기본 조작부터 익히고, 초보자용 공략을 참고하면 훨씬 편해요. 어떤 장르를 좋아하는지도 알려주시면 더 잘 추천해드릴게요!',
            createdAt: '2026-11-11 12:30:00'
          }
        ];
        localStorage.setItem(STORAGE_KEYS.COMMENTS, JSON.stringify(defaultComments));
      }

      const demoPostUpdates = [
        { id: 'p_1', oldTitle: '🎉 모두의 다중 게시판에 오신 것을 환영합니다!', title: '🎮 플레이어 라운지에 오신 것을 환영합니다!', content: '안녕하세요! 게임을 좋아하는 플레이어들이 모여 이야기 나누는 공간입니다.\n\n게임 소식은 공지사항에서, 플레이 경험은 자유게시판에서 나눠보세요. 막히는 부분은 게임 Q&A에 질문하고, 도움이 된 공략과 팁은 다른 플레이어들과 공유할 수 있습니다.\n\n좋아하는 게임이 달라도 서로 존중하며 즐겁게 소통해요!' },
        { id: 'p_2', oldTitle: '요즘 가장 재미있게 플레이 중인 게임은 무엇인가요?', title: '마인크래프트 생존 모드, 첫날에 뭐부터 하세요?', content: '새 월드에서 생존을 시작하면 첫날에 무엇부터 준비하시나요?\n저는 나무와 돌 도구를 먼저 모으고 밤이 오기 전에 간단한 집을 만들어요. 초반 생존에 유용한 팁이 있다면 알려주세요!', gameName: '마인크래프트' },
        { id: 'p_3', oldTitle: '자바스크립트에서 localStorage 데이터 크기 한계가 얼마나 되나요?', title: '친구들과 가볍게 즐길 협동 게임을 추천해주세요', content: '주말에 친구들과 같이 할 협동 게임을 찾고 있습니다.\n인원은 3~4명이고, 처음 하는 사람도 쉽게 적응할 수 있는 게임이면 좋겠어요. 직접 해본 게임 중 재미있었던 작품과 추천 이유를 알려주세요!' },
        { id: 'p_4', oldTitle: '업무 효율 200% 올려주는 유용한 단축키 모음 팁', title: '처음 만난 파티와도 편하게 소통하는 방법', content: '온라인 파티에서는 짧고 분명한 콜아웃이 큰 도움이 됩니다.\n\n- 필요한 정보부터 간결하게 전달하기\n- 실수했을 때 탓하기보다 다음 행동을 함께 정하기\n- 음성 채팅이 부담스럽다면 게임 내 핑과 채팅 활용하기\n- 팀원마다 플레이 방식이 다를 수 있다는 점 존중하기\n\n즐거운 플레이는 좋은 소통에서 시작됩니다!' }
      ];
      const posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
      let postsChanged = false;
      posts.forEach(post => {
        const update = demoPostUpdates.find(item => item.id === post.id);
        if (update && (post.title === update.oldTitle || post.title === update.title) && post.updatedAt === post.createdAt) {
          post.title = update.title;
          post.content = update.content;
          if (update.gameName) post.gameName = update.gameName;
          postsChanged = true;
        }
      });
      if (postsChanged) localStorage.setItem(STORAGE_KEYS.POSTS, JSON.stringify(posts));

      const demoCommentUpdates = [
        { id: 'c_1', oldContent: '게시판 깔끔하고 예쁘네요! 자주 이용하겠습니다.', content: '게임 좋아하는 사람들과 편하게 이야기 나눌 수 있어서 좋네요. 자주 올게요!' },
        { id: 'c_2', oldContent: '쌀쌀할 땐 순대국밥에 깍두기 국물 얹어 먹는 게 최고죠 ㅎㅎ', content: '저는 요즘 친구들이랑 하는 협동 게임에 푹 빠졌어요. 같이 하면 더 재미있더라고요!' },
        { id: 'c_3', oldContent: '대부분의 모던 브라우저에서 오리진당 약 5MB~10MB를 할당합니다. 더 큰 데이터나 구조화된 객체를 클라이언트 측에서 다루려면 IndexedDB를 추천합니다!', content: '처음 시작할 때는 튜토리얼과 기본 조작부터 익히고, 초보자용 공략을 참고하면 훨씬 편해요. 어떤 장르를 좋아하는지도 알려주시면 더 잘 추천해드릴게요!' }
      ];
      const comments = JSON.parse(localStorage.getItem(STORAGE_KEYS.COMMENTS) || '[]');
      let commentsChanged = false;
      comments.forEach(comment => {
        const update = demoCommentUpdates.find(item => item.id === comment.id);
        if (update && comment.content === update.oldContent) {
          comment.content = update.content;
          commentsChanged = true;
        }
      });
      if (commentsChanged) localStorage.setItem(STORAGE_KEYS.COMMENTS, JSON.stringify(comments));
    }

    class MultiBoardApp {
      constructor() {
        this.currentBoard = 'all';
        this.currentGameName = '';
        this.currentView = 'list'; // 'list' | 'detail' | 'editor'
        this.currentPostId = null;
        this.searchQuery = '';
        this.currentSort = 'newest';
        this.currentPage = 1;
        this.postsPerPage = 6;
        this.currentUser = null;
        this.confirmCallback = null;
        this.editingCommentId = null;

        this.init();
      }

      init() {
        seedInitialData();
        this.loadSession();
        this.renderAuthNav();
        this.renderBoardTabs();
        this.renderEditorBoardOptions();
        this.renderGameOptions();
        this.renderPopularGames();
        this.renderListView();
      }

      // ==================== 인증 및 세션 관리 ====================
      loadSession() {
        try {
          const session = localStorage.getItem(STORAGE_KEYS.SESSION);
          this.currentUser = session ? JSON.parse(session) : null;
        } catch (e) {
          this.currentUser = null;
        }
      }

      setSession(user) {
        this.currentUser = user;
        if (user) {
          localStorage.setItem(STORAGE_KEYS.SESSION, JSON.stringify(user));
        } else {
          localStorage.removeItem(STORAGE_KEYS.SESSION);
        }
        this.renderAuthNav();
        // 현재 화면 리렌더링
        if (this.currentView === 'detail') {
          this.renderDetailView(this.currentPostId, false);
        }
      }

      renderAuthNav() {
        const container = document.getElementById('authNavContainer');
        if (!container) return;

        if (this.currentUser) {
          const isAdmin = this.currentUser.role === 'admin';
          container.innerHTML = `
            <div class="flex items-center gap-2">
              <div class="w-8 h-8 rounded-full bg-blue-100 text-blue-700 flex items-center justify-center font-bold text-xs ring-2 ring-blue-500/20">
                ${this.escapeHtml(this.currentUser.nickname.slice(0, 1))}
              </div>
              <div class="hidden sm:flex flex-col text-left">
                <span class="text-xs font-bold text-slate-800 flex items-center gap-1">
                  ${this.escapeHtml(this.currentUser.nickname)}
                  ${isAdmin ? '<span class="px-1 py-0.2 text-[10px] bg-rose-100 text-rose-700 rounded font-bold">관리자</span>' : ''}
                </span>
                <span class="text-[10px] text-slate-400">@${this.escapeHtml(this.currentUser.username)}</span>
              </div>
              <button onclick="app.logout()" class="ml-1 px-3 py-1.5 text-xs text-slate-600 hover:text-rose-600 hover:bg-rose-50 border border-slate-200 rounded-lg transition font-medium">
                로그아웃
              </button>
            </div>
          `;
        } else {
          container.innerHTML = `
            <button onclick="app.openModal('loginModal')" class="whitespace-nowrap px-3.5 py-1.5 text-xs font-semibold text-slate-700 hover:text-blue-600 transition">
              로그인
            </button>
            <button onclick="app.openModal('registerModal')" class="whitespace-nowrap px-3.5 py-1.5 text-xs font-semibold bg-slate-900 hover:bg-slate-800 text-white rounded-lg transition shadow-xs">
              회원가입
            </button>
          `;
        }
      }

      handleLogin(e) {
        e.preventDefault();
        const username = document.getElementById('loginUsername').value.trim();
        const password = document.getElementById('loginPassword').value.trim();

        const users = JSON.parse(localStorage.getItem(STORAGE_KEYS.USERS) || '[]');
        const target = users.find(u => u.username === username && u.password === password);

        if (!target) {
          this.toast('아이디 또는 비밀번호가 일치하지 않습니다.', 'error');
          return;
        }

        this.setSession(target);
        this.closeModal('loginModal');
        this.toast(`${target.nickname}님 환영합니다!`, 'success');
        document.getElementById('loginUsername').value = '';
        document.getElementById('loginPassword').value = '';
      }

      quickLogin(username) {
        const users = JSON.parse(localStorage.getItem(STORAGE_KEYS.USERS) || '[]');
        const target = users.find(u => u.username === username);
        if (target) {
          this.setSession(target);
          this.closeModal('loginModal');
          this.toast(`${target.nickname} 계정으로 로그인되었습니다.`, 'success');
        }
      }

      logout() {
        const name = this.currentUser ? this.currentUser.nickname : '';
        this.setSession(null);
        this.toast(`${name}님 로그아웃 되었습니다.`, 'info');
      }

      handleRegister(e) {
        e.preventDefault();
        const username = document.getElementById('regUsername').value.trim();
        const nickname = document.getElementById('regNickname').value.trim();
        const password = document.getElementById('regPassword').value.trim();
        const confirm = document.getElementById('regPasswordConfirm').value.trim();

        if (password !== confirm) {
          this.toast('비밀번호가 일치하지 않습니다.', 'warning');
          return;
        }

        const users = JSON.parse(localStorage.getItem(STORAGE_KEYS.USERS) || '[]');
        if (users.some(u => u.username.toLowerCase() === username.toLowerCase())) {
          this.toast('이미 존재하는 아이디입니다.', 'error');
          return;
        }
        if (users.some(u => u.nickname.toLowerCase() === nickname.toLowerCase())) {
          this.toast('이미 사용 중인 닉네임입니다.', 'warning');
          return;
        }

        const newUser = {
          id: 'u_' + Date.now(),
          username,
          password,
          nickname,
          role: 'user',
          createdAt: this.formatDate(new Date())
        };

        users.push(newUser);
        localStorage.setItem(STORAGE_KEYS.USERS, JSON.stringify(users));

        this.setSession(newUser);
        this.closeModal('registerModal');
        this.toast(`회원가입이 완료되었습니다! 환영합니다, ${nickname}님!`, 'success');

        document.getElementById('regUsername').value = '';
        document.getElementById('regNickname').value = '';
        document.getElementById('regPassword').value = '';
        document.getElementById('regPasswordConfirm').value = '';
      }

      // ==================== 게시판 네비게이션 탭 ====================
      renderBoardTabs() {
        const nav = document.getElementById('boardTabsNav');
        if (!nav) return;

        let posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
        if (this.currentGameName) {
          const gameName = this.currentGameName.toLocaleLowerCase();
          posts = posts.filter(post => (post.gameName || '').toLocaleLowerCase() === gameName);
        }

        nav.innerHTML = BOARDS.map(b => {
          const isActive = this.currentBoard === b.id;
          const count = b.id === 'all' 
            ? posts.length 
            : posts.filter(p => p.boardId === b.id).length;

          return `
            <button onclick="app.selectBoard('${b.id}')"
                    class="flex items-center gap-1.5 px-3.5 py-2.5 text-sm font-semibold border-b-2 transition-all whitespace-nowrap ${
                      isActive 
                        ? 'border-blue-600 text-blue-600' 
                        : 'border-transparent text-slate-500 hover:text-slate-800 hover:border-slate-300'
                    }">
              <span>${b.icon}</span>
              <span>${b.name}</span>
              <span class="text-[11px] px-1.5 py-0.5 rounded-full ${
                isActive ? 'bg-blue-100 text-blue-700' : 'bg-slate-100 text-slate-500'
              }">${count}</span>
            </button>
          `;
        }).join('');

        const currentMeta = BOARDS.find(b => b.id === this.currentBoard) || BOARDS[0];
        document.getElementById('currentBoardTitle').innerHTML = this.currentGameName
          ? `🎮 ${this.escapeHtml(this.currentGameName)} · ${currentMeta.name}`
          : `${currentMeta.icon} ${currentMeta.name}`;
        document.getElementById('currentBoardDesc').innerHTML = this.currentGameName
          ? `${this.escapeHtml(this.currentGameName)} 관련 대화와 공략을 모아봅니다. <button onclick="app.clearGameFilter()" class="ml-1 text-blue-600 hover:underline font-semibold">게임 검색 초기화</button>`
          : currentMeta.desc;
      }

      selectBoard(boardId) {
        this.currentBoard = boardId;
        this.currentPage = 1;
        this.navigateToList(boardId);
      }

      renderGameOptions() {
        const options = document.getElementById('gameCatalogOptions');
        if (options) options.innerHTML = GAME_CATALOG.map(game => `<option value="${this.escapeHtml(game.name)}"></option>`).join('');
      }

      renderPopularGames() {
        const container = document.getElementById('popularGameButtons');
        if (!container) return;
        container.innerHTML = GAME_CATALOG.slice(0, 6).map(game => `
          <button type="button" onclick="app.selectGameButton(this)" data-game-name="${this.escapeHtml(game.name)}"
                  class="shrink-0 px-3 py-1.5 bg-white border border-slate-200 hover:border-blue-300 hover:text-blue-700 text-xs font-medium text-slate-600 rounded-full transition">
            ${this.escapeHtml(game.name)} <span class="text-slate-400">${this.escapeHtml(game.platform)}</span>
          </button>
        `).join('');
      }

      searchGames(query) {
        const results = document.getElementById('gameSearchResults');
        const popular = document.getElementById('popularGameButtons');
        if (!results || !popular) return;
        const normalizedQuery = query.trim().toLocaleLowerCase();
        if (!normalizedQuery) {
          results.classList.add('hidden');
          results.innerHTML = '';
          popular.classList.remove('hidden');
          return;
        }

        popular.classList.add('hidden');
        const matches = GAME_CATALOG.filter(game => `${game.name} ${game.platform} ${game.keywords}`.toLocaleLowerCase().includes(normalizedQuery));
        const posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
        const knownNames = [...new Set(posts.map(post => post.gameName).filter(Boolean))]
          .filter(name => name.toLocaleLowerCase().includes(normalizedQuery) && !matches.some(game => game.name.toLocaleLowerCase() === name.toLocaleLowerCase()))
          .map(name => ({ name, platform: '기존 대화 있음' }));
        const suggestions = [...matches, ...knownNames];

        results.innerHTML = suggestions.map(game => `
          <button type="button" onclick="app.selectGameButton(this)" data-game-name="${this.escapeHtml(game.name)}"
                  class="w-full flex items-center justify-between gap-3 px-4 py-3 text-left hover:bg-blue-50 transition border-b border-slate-100 last:border-b-0">
            <span class="text-sm font-semibold text-slate-800">${this.escapeHtml(game.name)}</span>
            <span class="text-xs text-slate-500">${this.escapeHtml(game.platform)}</span>
          </button>
        `).join('');

        const hasExactMatch = suggestions.some(game => game.name.toLocaleLowerCase() === normalizedQuery);
        if (!hasExactMatch && suggestions.length === 0) {
          results.innerHTML = `
            <button type="button" onclick="app.selectGameButton(this)" data-game-name="${this.escapeHtml(query.trim())}"
                    class="w-full flex items-center justify-between gap-3 px-4 py-3 text-left hover:bg-blue-50 transition">
              <span class="text-sm font-semibold text-slate-800">“${this.escapeHtml(query.trim())}” 대화 찾기</span>
              <span class="text-xs text-slate-500">직접 입력</span>
            </button>
          `;
        }
        results.classList.remove('hidden');
      }

      selectGameButton(button) {
        this.selectGame(button.dataset.gameName || '');
      }

      applyGameSearch() {
        const input = document.getElementById('gameSearchInput');
        const query = input.value.trim();
        if (!query) {
          input.focus();
          return;
        }

        const normalizedQuery = query.toLocaleLowerCase();
        const exactMatch = GAME_CATALOG.find(game => game.name.toLocaleLowerCase() === normalizedQuery);
        const matches = GAME_CATALOG.filter(game => `${game.name} ${game.platform} ${game.keywords}`.toLocaleLowerCase().includes(normalizedQuery));
        if (exactMatch || matches.length === 1 || matches.length === 0) {
          this.selectGame((exactMatch || matches[0] || { name: query }).name);
        } else {
          this.searchGames(query);
        }
      }

      selectGame(gameName) {
        this.currentGameName = gameName.trim();
        this.currentBoard = 'all';
        this.currentPage = 1;
        this.searchQuery = '';
        document.getElementById('gameSearchInput').value = this.currentGameName;
        document.getElementById('gameSearchResults').classList.add('hidden');
        document.getElementById('popularGameButtons').classList.toggle('hidden', Boolean(this.currentGameName));
        document.getElementById('searchInput').value = '';
        document.getElementById('clearSearchBtn').classList.add('hidden');
        this.navigateToList(this.currentBoard);
      }

      clearGameFilter() {
        this.currentGameName = '';
        document.getElementById('gameSearchInput').value = '';
        document.getElementById('popularGameButtons').classList.remove('hidden');
        this.currentPage = 1;
        this.navigateToList(this.currentBoard);
      }

      renderEditorBoardOptions() {
        const select = document.getElementById('formBoardSelect');
        if (!select) return;
        const writableBoards = BOARDS.filter(b => b.id !== 'all');
        select.innerHTML = writableBoards.map(b => `
          <option value="${b.id}">${b.icon} ${b.name}</option>
        `).join('');
      }

      // ==================== 뷰 전환 ====================
      navigateToList(boardId = null) {
        if (boardId) this.currentBoard = boardId;
        this.currentView = 'list';
        this.currentPostId = null;

        document.getElementById('boardHeaderSection').classList.remove('hidden');
        document.getElementById('listView').classList.remove('hidden');
        document.getElementById('detailView').classList.add('hidden');
        document.getElementById('editorView').classList.add('hidden');

        this.renderBoardTabs();
        this.renderListView();
        window.scrollTo({ top: 0, behavior: 'smooth' });
      }

      openDetail(postId) {
        this.currentView = 'detail';
        this.currentPostId = postId;

        document.getElementById('boardHeaderSection').classList.add('hidden');
        document.getElementById('listView').classList.add('hidden');
        document.getElementById('detailView').classList.remove('hidden');
        document.getElementById('editorView').classList.add('hidden');

        this.renderDetailView(postId, true);
        window.scrollTo({ top: 0, behavior: 'smooth' });
      }

      backToList() {
        this.navigateToList(this.currentBoard);
      }

      openEditor(postId = null) {
        if (!this.currentUser) {
          this.toast('게시글을 작성하려면 로그인이 필요합니다.', 'warning');
          this.openModal('loginModal');
          return;
        }

        this.currentView = 'editor';
        document.getElementById('boardHeaderSection').classList.add('hidden');
        document.getElementById('listView').classList.add('hidden');
        document.getElementById('detailView').classList.add('hidden');
        document.getElementById('editorView').classList.remove('hidden');

        const titleInput = document.getElementById('formTitleInput');
        const contentInput = document.getElementById('formContentInput');
        const gameInput = document.getElementById('formGameInput');
        const boardSelect = document.getElementById('formBoardSelect');
        const editIdInput = document.getElementById('editPostId');
        const pageTitle = document.getElementById('editorPageTitle');
        const submitBtn = document.getElementById('submitPostBtn');

        if (postId) {
          // 수정 모드
          const posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
          const post = posts.find(p => p.id === postId);

          if (!post) {
            this.toast('존재하지 않는 게시글입니다.', 'error');
            this.backToList();
            return;
          }

          // 권한 확인: 작성자 본인 확인
          if (post.authorId !== this.currentUser.id && this.currentUser.role !== 'admin') {
            this.toast('작성자 본인만 수정할 수 있습니다.', 'error');
            this.backToList();
            return;
          }

          editIdInput.value = post.id;
          boardSelect.value = post.boardId;
          gameInput.value = post.gameName || '';
          titleInput.value = post.title;
          contentInput.value = post.content;
          pageTitle.innerText = '게시글 수정';
          submitBtn.innerText = '수정 완료';
        } else {
          // 신규 작성 모드
          editIdInput.value = '';
          boardSelect.value = this.currentBoard !== 'all' ? this.currentBoard : 'free';
          gameInput.value = this.currentGameName;
          titleInput.value = '';
          contentInput.value = '';
          pageTitle.innerText = '새 게시글 작성';
          submitBtn.innerText = '게시글 등록';
        }

        document.getElementById('contentLengthHint').innerText = `${contentInput.value.length.toLocaleString()} / 5,000자`;
        window.scrollTo({ top: 0, behavior: 'smooth' });
      }

      openEditorForEdit() {
        if (this.currentPostId) {
          this.openEditor(this.currentPostId);
        }
      }

      cancelEditor() {
        if (this.currentPostId) {
          this.openDetail(this.currentPostId);
        } else {
          this.backToList();
        }
      }

      // ==================== 목록 뷰 렌더링 ====================
      renderListView() {
        const container = document.getElementById('postListContainer');
        const pagination = document.getElementById('paginationContainer');
        if (!container) return;

        let posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
        const comments = JSON.parse(localStorage.getItem(STORAGE_KEYS.COMMENTS) || '[]');

        // 게시판 필터
        if (this.currentBoard !== 'all') {
          posts = posts.filter(p => p.boardId === this.currentBoard);
        }

        if (this.currentGameName) {
          const gameName = this.currentGameName.toLocaleLowerCase();
          posts = posts.filter(p => (p.gameName || '').toLocaleLowerCase() === gameName);
        }

        // 검색 필터
        if (this.searchQuery) {
          const q = this.searchQuery.toLowerCase();
          posts = posts.filter(p => 
            p.title.toLowerCase().includes(q) ||
            p.content.toLowerCase().includes(q) ||
            p.authorNickname.toLowerCase().includes(q) ||
            (p.gameName || '').toLowerCase().includes(q)
          );
        }

        // 정렬
        if (this.currentSort === 'newest') {
          posts.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
        } else if (this.currentSort === 'views') {
          posts.sort((a, b) => (b.views || 0) - (a.views || 0));
        } else if (this.currentSort === 'comments') {
          posts.sort((a, b) => {
            const countA = comments.filter(c => c.postId === a.id).length;
            const countB = comments.filter(c => c.postId === b.id).length;
            return countB - countA;
          });
        }

        if (posts.length === 0) {
          container.innerHTML = `
            <div class="py-16 text-center text-slate-400 space-y-3">
              <div class="w-16 h-16 mx-auto rounded-full bg-slate-100 flex items-center justify-center text-slate-400">
                <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.172 16.172a4 4 0 015.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
                </svg>
              </div>
              <p class="text-sm font-medium text-slate-500">등록된 게시글이 없습니다.</p>
              ${this.currentGameName ? `<p class="text-xs text-slate-400">${this.escapeHtml(this.currentGameName)} 관련 첫 대화를 시작해보세요.</p><button onclick="app.openEditor()" class="text-xs text-blue-600 font-semibold underline">이 게임으로 글쓰기</button>` : ''}
              ${this.searchQuery ? '<button onclick="app.clearSearch()" class="text-xs text-blue-600 font-semibold underline">검색어 초기화</button>' : ''}
            </div>
          `;
          pagination.innerHTML = '';
          return;
        }

        // 페이지네이션 슬라이스
        const totalPages = Math.ceil(posts.length / this.postsPerPage);
        if (this.currentPage > totalPages) this.currentPage = totalPages;
        const startIndex = (this.currentPage - 1) * this.postsPerPage;
        const pagedPosts = posts.slice(startIndex, startIndex + this.postsPerPage);

        container.innerHTML = pagedPosts.map(post => {
          const boardMeta = BOARDS.find(b => b.id === post.boardId) || { name: '일반', color: 'bg-slate-100 text-slate-700' };
          const postComments = comments.filter(c => c.postId === post.id);
          const isNotice = post.boardId === 'notice';

          return `
            <article onclick="app.openDetail('${post.id}')"
                     class="group p-4 sm:p-5 flex flex-col sm:flex-row sm:items-center justify-between gap-3 hover:bg-blue-50/40 transition cursor-pointer ${
                       isNotice ? 'bg-rose-50/20' : ''
                     }">
              <div class="space-y-1.5 flex-1 min-w-0 pr-2">
                <div class="flex items-center gap-2 flex-wrap">
                  <span class="px-2 py-0.5 text-xs font-semibold rounded-md border ${boardMeta.color}">
                    ${boardMeta.name}
                  </span>
                  ${post.gameName ? `<span class="px-2 py-0.5 text-xs font-semibold rounded-md bg-blue-50 text-blue-700 border border-blue-100">${this.escapeHtml(post.gameName)}</span>` : ''}
                  <h3 class="font-bold text-slate-900 group-hover:text-blue-600 transition truncate text-base">
                    ${this.escapeHtml(post.title)}
                  </h3>
                  ${postComments.length > 0 ? `
                    <span class="text-xs font-bold text-blue-600 bg-blue-50 px-1.5 py-0.2 rounded-full">
                      [${postComments.length}]
                    </span>
                  ` : ''}
                </div>
                <p class="text-xs text-slate-500 line-clamp-1 break-words">
                  ${this.escapeHtml(post.content.replace(/\n/g, ' '))}
                </p>
              </div>

              <div class="flex items-center justify-between sm:justify-end gap-4 text-xs text-slate-400 shrink-0 pt-2 sm:pt-0 border-t sm:border-t-0 border-slate-100">
                <span class="font-medium text-slate-700 flex items-center gap-1.5">
                  <span class="w-5 h-5 rounded-full bg-slate-100 text-slate-600 inline-flex items-center justify-center font-bold text-[10px]">
                    ${this.escapeHtml(post.authorNickname.slice(0, 1))}
                  </span>
                  ${this.escapeHtml(post.authorNickname)}
                </span>
                <span>${this.formatTimeAgo(post.createdAt)}</span>
                <span class="flex items-center gap-1" title="조회수">
                  <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"/>
                  </svg>
                  ${post.views || 0}
                </span>
              </div>
            </article>
          `;
        }).join('');

        // 페이지네이션 렌더링
        this.renderPagination(totalPages);
      }

      renderPagination(totalPages) {
        const container = document.getElementById('paginationContainer');
        if (!container || totalPages <= 1) {
          if (container) container.innerHTML = '';
          return;
        }

        let html = '';
        html += `
          <button onclick="app.changePage(${this.currentPage - 1})" ${this.currentPage === 1 ? 'disabled' : ''}
                  class="px-3 py-1.5 text-xs rounded-lg border border-slate-200 text-slate-600 hover:bg-slate-100 disabled:opacity-40 disabled:hover:bg-transparent">
            이전
          </button>
        `;

        for (let i = 1; i <= totalPages; i++) {
          const isActive = this.currentPage === i;
          html += `
            <button onclick="app.changePage(${i})"
                    class="w-8 h-8 text-xs font-semibold rounded-lg transition ${
                      isActive 
                        ? 'bg-blue-600 text-white shadow-xs' 
                        : 'text-slate-600 hover:bg-slate-100'
                    }">
              ${i}
            </button>
          `;
        }

        html += `
          <button onclick="app.changePage(${this.currentPage + 1})" ${this.currentPage === totalPages ? 'disabled' : ''}
                  class="px-3 py-1.5 text-xs rounded-lg border border-slate-200 text-slate-600 hover:bg-slate-100 disabled:opacity-40 disabled:hover:bg-transparent">
            다음
          </button>
        `;

        container.innerHTML = html;
      }

      changePage(page) {
        this.currentPage = page;
        this.renderListView();
        window.scrollTo({ top: 0, behavior: 'smooth' });
      }

      handleSearch() {
        const input = document.getElementById('searchInput');
        this.searchQuery = input.value.trim();
        const clearBtn = document.getElementById('clearSearchBtn');
        if (this.searchQuery) {
          clearBtn.classList.remove('hidden');
        } else {
          clearBtn.classList.add('hidden');
        }
        this.currentPage = 1;
        this.renderListView();
      }

      clearSearch() {
        const input = document.getElementById('searchInput');
        input.value = '';
        this.searchQuery = '';
        document.getElementById('clearSearchBtn').classList.add('hidden');
        this.currentPage = 1;
        this.renderListView();
      }

      handleSortChange(sort) {
        this.currentSort = sort;
        this.currentPage = 1;
        this.renderListView();
      }

      // ==================== 상세 뷰 렌더링 ====================
      renderDetailView(postId, incrementViews = false) {
        const posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
        const postIndex = posts.findIndex(p => p.id === postId);

        if (postIndex === -1) {
          this.toast('게시글을 찾을 수 없습니다.', 'error');
          this.backToList();
          return;
        }

        const post = posts[postIndex];

        // 조회수 증가 처리
        if (incrementViews) {
          post.views = (post.views || 0) + 1;
          posts[postIndex] = post;
          localStorage.setItem(STORAGE_KEYS.POSTS, JSON.stringify(posts));
        }

        const boardMeta = BOARDS.find(b => b.id === post.boardId) || { name: '게시판', color: 'bg-slate-100 text-slate-700' };

        // 뱃지 및 메타정보 설정
        const badgeEl = document.getElementById('detailBoardBadge');
        badgeEl.className = `px-2.5 py-0.5 text-xs font-semibold rounded-md border ${boardMeta.color}`;
        badgeEl.innerText = boardMeta.name;

        const gameBadge = document.getElementById('detailGameBadge');
        if (post.gameName) {
          gameBadge.innerText = post.gameName;
          gameBadge.classList.remove('hidden');
        } else {
          gameBadge.classList.add('hidden');
        }

        document.getElementById('detailDate').innerText = `작성일: ${post.createdAt} ${post.updatedAt !== post.createdAt ? '(수정됨)' : ''}`;
        document.getElementById('detailTitle').innerText = post.title;
        document.getElementById('detailAuthorName').innerText = post.authorNickname;
        document.getElementById('detailAuthorAvatar').innerText = post.authorNickname.slice(0, 1);
        document.getElementById('detailAuthorSub').innerText = post.authorId === 'u_admin' ? '운영팀 공식' : '회원';
        document.getElementById('detailViews').innerText = post.views || 0;
        document.getElementById('detailContent').innerText = post.content;

        // **작성자 본인 권한 검증: 수정/삭제 버튼 노출 여부**
        const authorActions = document.getElementById('authorActionButtons');
        const isAuthor = this.currentUser && (this.currentUser.id === post.authorId || this.currentUser.role === 'admin');

        if (isAuthor) {
          authorActions.classList.remove('hidden');
          authorActions.classList.add('flex');
        } else {
          authorActions.classList.add('hidden');
          authorActions.classList.remove('flex');
        }

        // 댓글 렌더링
        this.renderComments(postId);
      }

      // ==================== 댓글 기능 ====================
      renderComments(postId) {
        const allComments = JSON.parse(localStorage.getItem(STORAGE_KEYS.COMMENTS) || '[]');
        const comments = allComments.filter(c => c.postId === postId);

        document.getElementById('detailCommentsCount').innerText = comments.length;
        document.getElementById('commentSectionCount').innerText = comments.length;

        // 댓글 입력창 영역
        const formWrapper = document.getElementById('commentFormWrapper');
        if (this.currentUser) {
          formWrapper.innerHTML = `
            <div class="flex items-start gap-3">
              <div class="w-8 h-8 rounded-full bg-blue-100 text-blue-700 flex items-center justify-center font-bold text-xs shrink-0 mt-1">
                ${this.escapeHtml(this.currentUser.nickname.slice(0, 1))}
              </div>
              <div class="flex-1 space-y-2">
                <textarea id="commentInput" rows="2" placeholder="${this.escapeHtml(this.currentUser.nickname)}님, 댓글을 남겨보세요..."
                          class="w-full px-3.5 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:bg-white focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 transition resize-none"></textarea>
                <div class="flex justify-end">
                  <button onclick="app.handleCreateComment()" class="px-4 py-2 bg-blue-600 hover:bg-blue-700 active:scale-95 text-white text-xs font-semibold rounded-lg shadow-sm transition">
                    댓글 등록
                  </button>
                </div>
              </div>
            </div>
          `;
        } else {
          formWrapper.innerHTML = `
            <div onclick="app.openModal('loginModal')" class="p-4 bg-slate-50 border border-slate-200 border-dashed rounded-xl text-center text-xs text-slate-500 hover:bg-blue-50/50 hover:border-blue-300 transition cursor-pointer">
              <p class="font-medium text-slate-700">댓글을 작성하려면 로그인이 필요합니다.</p>
              <p class="text-blue-600 font-semibold mt-0.5">여기를 클릭하여 로그인하세요</p>
            </div>
          `;
        }

        // 댓글 목록 영역
        const listContainer = document.getElementById('commentListContainer');
        if (comments.length === 0) {
          listContainer.innerHTML = `
            <div class="text-center py-8 text-xs text-slate-400">
              아직 작성된 댓글이 없습니다. 첫 번째 댓글을 남겨보세요!
            </div>
          `;
          return;
        }

        // 댓글 최신순 혹은 등록순(오래된 순)
        comments.sort((a, b) => new Date(a.createdAt) - new Date(b.createdAt));

        listContainer.innerHTML = comments.map(c => {
          const isCommentAuthor = this.currentUser && (this.currentUser.id === c.authorId || this.currentUser.role === 'admin');
          const isEditing = this.editingCommentId === c.id;

          return `
            <div class="group flex items-start justify-between gap-3 p-3.5 rounded-xl bg-slate-50/70 hover:bg-slate-100/60 transition">
              <div class="flex items-start gap-3">
                <div class="w-7 h-7 rounded-full bg-slate-200 text-slate-700 flex items-center justify-center font-bold text-xs shrink-0 mt-0.5">
                  ${this.escapeHtml(c.authorNickname.slice(0, 1))}
                </div>
                <div class="space-y-1">
                  <div class="flex items-center gap-2">
                    <span class="text-xs font-bold text-slate-800">${this.escapeHtml(c.authorNickname)}</span>
                    <span class="text-[11px] text-slate-400">${this.formatTimeAgo(c.createdAt)}</span>
                    ${c.updatedAt ? '<span class="text-[11px] text-slate-400">수정됨</span>' : ''}
                  </div>
                  ${isEditing ? `
                    <div class="space-y-2">
                      <textarea id="editCommentInput_${c.id}" rows="3" maxlength="1000"
                                class="w-full min-w-[240px] px-3 py-2 text-sm bg-white border border-slate-300 rounded-lg focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-100 resize-y">${this.escapeHtml(c.content)}</textarea>
                      <div class="flex gap-2">
                        <button onclick="app.handleUpdateComment('${c.id}')" class="px-3 py-1.5 bg-blue-600 hover:bg-blue-700 text-white text-xs font-semibold rounded-lg">저장</button>
                        <button onclick="app.cancelEditComment()" class="px-3 py-1.5 border border-slate-300 text-slate-600 text-xs font-semibold rounded-lg hover:bg-white">취소</button>
                      </div>
                    </div>
                  ` : `
                    <p class="text-xs sm:text-sm text-slate-700 whitespace-pre-wrap break-words leading-relaxed">
                      ${this.escapeHtml(c.content)}
                    </p>
                  `}
                </div>
              </div>

              ${isCommentAuthor ? `
                ${!isEditing ? `
                  <div class="flex items-center gap-1 shrink-0">
                    <button onclick="app.startEditComment('${c.id}')" class="text-slate-400 hover:text-blue-600 p-1 text-xs transition" title="댓글 수정">수정</button>
                    <button onclick="app.handleDeleteComment('${c.id}')" class="text-slate-400 hover:text-rose-600 p-1 text-xs transition" title="댓글 삭제">
                      <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
                      </svg>
                    </button>
                  </div>
                ` : ''}
              ` : ''}
            </div>
          `;
        }).join('');
      }

      startEditComment(commentId) {
        if (!this.currentUser) return;
        const comments = JSON.parse(localStorage.getItem(STORAGE_KEYS.COMMENTS) || '[]');
        const comment = comments.find(c => c.id === commentId);
        if (!comment) return;
        if (comment.authorId !== this.currentUser.id && this.currentUser.role !== 'admin') {
          this.toast('댓글 작성자 또는 관리자만 수정할 수 있습니다.', 'error');
          return;
        }
        this.editingCommentId = commentId;
        this.renderComments(this.currentPostId);
        document.getElementById(`editCommentInput_${commentId}`)?.focus();
      }

      cancelEditComment() {
        this.editingCommentId = null;
        this.renderComments(this.currentPostId);
      }

      handleUpdateComment(commentId) {
        if (!this.currentUser) return;
        const comments = JSON.parse(localStorage.getItem(STORAGE_KEYS.COMMENTS) || '[]');
        const comment = comments.find(c => c.id === commentId);
        if (!comment) return;
        if (comment.authorId !== this.currentUser.id && this.currentUser.role !== 'admin') {
          this.toast('댓글 작성자 또는 관리자만 수정할 수 있습니다.', 'error');
          return;
        }

        const input = document.getElementById(`editCommentInput_${commentId}`);
        const content = input.value.trim();
        if (!content) {
          this.toast('댓글 내용을 입력해주세요.', 'warning');
          input.focus();
          return;
        }

        comment.content = content;
        comment.updatedAt = this.formatDate(new Date());
        localStorage.setItem(STORAGE_KEYS.COMMENTS, JSON.stringify(comments));
        this.editingCommentId = null;
        this.renderComments(this.currentPostId);
        this.toast('댓글이 수정되었습니다.', 'success');
      }

      handleCreateComment() {
        if (!this.currentUser) {
          this.toast('로그인이 필요합니다.', 'warning');
          this.openModal('loginModal');
          return;
        }

        const input = document.getElementById('commentInput');
        const content = input.value.trim();

        if (!content) {
          this.toast('댓글 내용을 입력해주세요.', 'warning');
          input.focus();
          return;
        }

        const allComments = JSON.parse(localStorage.getItem(STORAGE_KEYS.COMMENTS) || '[]');
        const newComment = {
          id: 'c_' + Date.now(),
          postId: this.currentPostId,
          authorId: this.currentUser.id,
          authorNickname: this.currentUser.nickname,
          content,
          createdAt: this.formatDate(new Date())
        };

        allComments.push(newComment);
        localStorage.setItem(STORAGE_KEYS.COMMENTS, JSON.stringify(allComments));

        input.value = '';
        this.renderComments(this.currentPostId);
        this.toast('댓글이 등록되었습니다.', 'success');
      }

      handleDeleteComment(commentId) {
        if (!this.currentUser) return;

        const allComments = JSON.parse(localStorage.getItem(STORAGE_KEYS.COMMENTS) || '[]');
        const target = allComments.find(c => c.id === commentId);

        if (!target) return;

        // 권한 검증: 본인 확인
        if (target.authorId !== this.currentUser.id && this.currentUser.role !== 'admin') {
          this.toast('본인이 작성한 댓글만 삭제할 수 있습니다.', 'error');
          return;
        }

        const updated = allComments.filter(c => c.id !== commentId);
        localStorage.setItem(STORAGE_KEYS.COMMENTS, JSON.stringify(updated));

        this.renderComments(this.currentPostId);
        this.toast('댓글이 삭제되었습니다.', 'info');
      }

      // ==================== 게시글 저장 (작성 / 수정) ====================
      handleSavePost(e) {
        e.preventDefault();

        if (!this.currentUser) {
          this.toast('로그인이 필요합니다.', 'warning');
          this.openModal('loginModal');
          return;
        }

        const editId = document.getElementById('editPostId').value;
        const boardId = document.getElementById('formBoardSelect').value;
        const gameName = document.getElementById('formGameInput').value.trim().slice(0, 50);
        const title = document.getElementById('formTitleInput').value.trim();
        const content = document.getElementById('formContentInput').value.trim();

        if (!title || !content) {
          this.toast('제목과 내용을 모두 입력해주세요.', 'warning');
          return;
        }

        const posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
        const now = this.formatDate(new Date());

        if (editId) {
          // 수정 로직
          const postIndex = posts.findIndex(p => p.id === editId);
          if (postIndex === -1) {
            this.toast('게시글을 찾을 수 없습니다.', 'error');
            return;
          }

          // **권한 검증: 작성자 본인 확인**
          if (posts[postIndex].authorId !== this.currentUser.id && this.currentUser.role !== 'admin') {
            this.toast('작성자 본인만 수정할 수 있습니다.', 'error');
            return;
          }

          posts[postIndex].boardId = boardId;
          posts[postIndex].gameName = gameName;
          posts[postIndex].title = title;
          posts[postIndex].content = content;
          posts[postIndex].updatedAt = now;

          localStorage.setItem(STORAGE_KEYS.POSTS, JSON.stringify(posts));
          this.toast('게시글이 성공적으로 수정되었습니다.', 'success');
          this.openDetail(editId);
        } else {
          // 신규 작성 로직
          const newPost = {
            id: 'p_' + Date.now(),
            boardId,
            gameName,
            title,
            content,
            authorId: this.currentUser.id,
            authorNickname: this.currentUser.nickname,
            views: 0,
            createdAt: now,
            updatedAt: now
          };

          posts.unshift(newPost);
          localStorage.setItem(STORAGE_KEYS.POSTS, JSON.stringify(posts));
          this.toast('새 게시글이 성공적으로 등록되었습니다.', 'success');
          this.currentBoard = boardId;
          this.currentGameName = gameName;
          this.openDetail(newPost.id);
        }
      }

      // ==================== 게시글 삭제 ====================
      confirmDeletePost() {
        if (!this.currentPostId || !this.currentUser) return;

        const posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
        const post = posts.find(p => p.id === this.currentPostId);

        if (!post) return;

        // **권한 검증**
        if (post.authorId !== this.currentUser.id && this.currentUser.role !== 'admin') {
          this.toast('본인이 작성한 글만 삭제할 수 있습니다.', 'error');
          return;
        }

        document.getElementById('confirmModalTitle').innerText = '게시글 삭제';
        document.getElementById('confirmModalMessage').innerText = '정말 이 게시글을 삭제하시겠습니까? 등록된 댓글도 함께 삭제되며 되돌릴 수 없습니다.';
        
        const confirmBtn = document.getElementById('confirmModalBtn');
        confirmBtn.onclick = () => {
          this.executeDeletePost(this.currentPostId);
          this.closeModal('confirmModal');
        };

        this.openModal('confirmModal');
      }

      executeDeletePost(postId) {
        let posts = JSON.parse(localStorage.getItem(STORAGE_KEYS.POSTS) || '[]');
        const target = posts.find(post => post.id === postId);
        if (!target || !this.currentUser || (target.authorId !== this.currentUser.id && this.currentUser.role !== 'admin')) {
          this.toast('작성자 본인 또는 관리자만 삭제할 수 있습니다.', 'error');
          return;
        }
        posts = posts.filter(p => p.id !== postId);
        localStorage.setItem(STORAGE_KEYS.POSTS, JSON.stringify(posts));

        // 댓글도 함께 정리
        let comments = JSON.parse(localStorage.getItem(STORAGE_KEYS.COMMENTS) || '[]');
        comments = comments.filter(c => c.postId !== postId);
        localStorage.setItem(STORAGE_KEYS.COMMENTS, JSON.stringify(comments));

        this.toast('게시글이 삭제되었습니다.', 'info');
        this.navigateToList(this.currentBoard);
      }

      // ==================== 모달 제어 ====================
      openModal(modalId) {
        const modal = document.getElementById(modalId);
        if (modal) {
          modal.classList.remove('hidden');
          // 첫 인풋 자동 포커스
          const input = modal.querySelector('input');
          if (input) setTimeout(() => input.focus(), 50);
        }
      }

      closeModal(modalId) {
        const modal = document.getElementById(modalId);
        if (modal) {
          modal.classList.add('hidden');
        }
      }

      switchModal(fromId, toId) {
        this.closeModal(fromId);
        this.openModal(toId);
      }

      // ==================== 토스트 알림 ====================
      toast(message, type = 'info') {
        const container = document.getElementById('toastContainer');
        if (!container) return;

        const toast = document.createElement('div');
        toast.className = `p-3.5 rounded-xl shadow-lg border text-xs sm:text-sm font-medium flex items-center justify-between gap-3 pointer-events-auto transform transition-all duration-300 translate-y-2 opacity-0`;

        let icon = '';
        if (type === 'success') {
          toast.classList.add('bg-emerald-50', 'text-emerald-900', 'border-emerald-200');
          icon = `<svg class="w-4 h-4 text-emerald-600 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>`;
        } else if (type === 'error') {
          toast.classList.add('bg-rose-50', 'text-rose-900', 'border-rose-200');
          icon = `<svg class="w-4 h-4 text-rose-600 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>`;
        } else if (type === 'warning') {
          toast.classList.add('bg-amber-50', 'text-amber-900', 'border-amber-200');
          icon = `<svg class="w-4 h-4 text-amber-600 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/></svg>`;
        } else {
          toast.classList.add('bg-slate-900', 'text-white', 'border-slate-800');
          icon = `<svg class="w-4 h-4 text-blue-400 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>`;
        }

        toast.innerHTML = `
          <div class="flex items-center gap-2">
            ${icon}
            <span>${this.escapeHtml(message)}</span>
          </div>
        `;

        container.appendChild(toast);

        // 애니메이션 효과
        requestAnimationFrame(() => {
          toast.classList.remove('translate-y-2', 'opacity-0');
        });

        setTimeout(() => {
          toast.classList.add('opacity-0', 'translate-y-2');
          setTimeout(() => toast.remove(), 300);
        }, 3000);
      }

      // ==================== 유틸리티 ====================
      escapeHtml(str) {
        if (!str) return '';
        return String(str)
          .replace(/&/g, '&amp;')
          .replace(/</g, '&lt;')
          .replace(/>/g, '&gt;')
          .replace(/"/g, '&quot;')
          .replace(/'/g, '&#039;');
      }

      formatDate(d) {
        const pad = n => String(n).padStart(2, '0');
        return `${d.getFullYear()}-${pad(d.getMonth() + 1)}-${pad(d.getDate())} ${pad(d.getHours())}:${pad(d.getMinutes())}:${pad(d.getSeconds())}`;
      }

      formatTimeAgo(dateStr) {
        try {
          const d = new Date(dateStr.replace(/-/g, '/'));
          const now = new Date();
          const diffSec = Math.floor((now - d) / 1000);

          if (diffSec < 60) return '방금 전';
          if (diffSec < 3600) return `${Math.floor(diffSec / 60)}분 전`;
          if (diffSec < 86400) return `${Math.floor(diffSec / 3600)}시간 전`;
          if (diffSec < 86400 * 7) return `${Math.floor(diffSec / 86400)}일 전`;
          return dateStr.split(' ')[0];
        } catch (e) {
          return dateStr;
        }
      }
    }

    // 전역 애플리케이션 인스턴스 초기화
    let app;
    document.addEventListener('DOMContentLoaded', () => {
      app = new MultiBoardApp();
    });
  </script>
</body>
</html>
