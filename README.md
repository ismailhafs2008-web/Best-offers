<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أفضل العروض الإعلانية</title>

<style>
* {
    box-sizing: border-box;
}

html {
    scroll-behavior: auto;
}

body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #f3f5f9;
    color: #172033;
}

header {
    background: linear-gradient(135deg, #101c36, #263f70);
    color: white;
    padding: 24px 16px;
    text-align: center;
}

header h1 {
    margin: 0 0 18px;
    font-size: clamp(22px, 4vw, 34px);
}

.navigation {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 14px;
    flex-wrap: wrap;
}

.navigation button {
    border: none;
    border-radius: 10px;
    padding: 12px 20px;
    background: #f5b82e;
    color: #172033;
    font-size: 19px;
    font-weight: bold;
    cursor: pointer;
}

.navigation button:active,
.side-controls button:active {
    transform: scale(.95);
}

#pageNumber {
    min-width: 110px;
    font-size: 18px;
    font-weight: bold;
}

main {
    padding: 22px 16px;
}

.section-title {
    margin: 0 0 18px;
    font-size: 22px;
}

.ad-container {
    width: 100%;
    overflow-x: auto;
    overflow-y: hidden;
    background: white;
    border: 1px solid #dce2ec;
    border-radius: 12px;
    padding: 14px;
    -webkit-overflow-scrolling: touch;
}

.ad-track {
    display: flex;
    flex-direction: row;
    direction: ltr;
    gap: 14px;
    width: max-content;
}

.ad-slot {
    flex: 0 0 280px;
    width: 280px;
    height: 220px;
    background: #fff;
    border: 1px solid #e0e5ee;
    border-radius: 10px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
}

.ad-slot .ad-content {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #9aa4b5;
    font-size: 14px;
}

.ad-slot footer {
    background: #f4f6fa;
    color: #69758a;
    padding: 8px;
    font-size: 12px;
    text-align: center;
}

.side-controls {
    position: fixed;
    left: 12px;
    bottom: 24px;
    z-index: 1000;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.side-controls button {
    width: 48px;
    height: 48px;
    border: none;
    border-radius: 50%;
    background: #172b50;
    color: white;
    font-size: 23px;
    box-shadow: 0 3px 12px #0002;
    cursor: pointer;
}

.side-controls button:hover {
    background: #31538d;
}

.page-info {
    margin-top: 18px;
    color: #647084;
    font-size: 14px;
    text-align: center;
}

@media (max-width: 600px) {
    header {
        padding: 20px 10px;
    }

    .navigation {
        gap: 8px;
    }

    .navigation button {
        padding: 11px 15px;
    }

    .ad-slot {
        flex-basis: 240px;
        width: 240px;
        height: 190px;
    }

    .side-controls {
        left: 8px;
        bottom: 16px;
    }

    .side-controls button {
        width: 44px;
        height: 44px;
    }
}
</style>
</head>

<body>

<header>
    <h1>نقدم لكم أفضل العروض الإعلانية في هذا الموسم</h1>

    <div class="navigation">
        <button id="prevPage" aria-label="الصفحة السابقة">❮</button>

        <span id="pageNumber">صفحة 0 / 999</span>

        <button id="nextPage" aria-label="الصفحة التالية">❯</button>
    </div>
</header>

<main>
    <h2 class="section-title">العروض الإعلانية</h2>

    <div class="ad-container" id="adContainer">
        <div class="ad-track" id="adTrack"></div>
    </div>

    <p class="page-info" id="pageInfo">
        الصفحة 0 — لا توجد إعلانات مضافة حاليًا.
    </p>
</main>

<div class="side-controls">
    <button id="scrollUp" aria-label="الصعود">↑</button>
    <button id="scrollDown" aria-label="الهبوط">↓</button>
</div>

<script>
const TOTAL_PAGES = 1000;
const ADS_PER_PAGE = 10;

let currentPage = 0;

const pageNumber = document.getElementById("pageNumber");
const pageInfo = document.getElementById("pageInfo");
const adTrack = document.getElementById("adTrack");
const adContainer = document.getElementById("adContainer");

// إنشاء أماكن فارغة للإعلانات دون إضافة عروض وهمية.
function renderPage() {
    adTrack.replaceChildren();

    for (let i = 0; i < ADS_PER_PAGE; i++) {
        const adNumber = currentPage * ADS_PER_PAGE + i;

        const slot = document.createElement("article");
        slot.className = "ad-slot";

        const content = document.createElement("div");
        content.className = "ad-content";

        const footer = document.createElement("footer");
        footer.textContent = "مساحة إعلانية " + adNumber;

        slot.appendChild(content);
        slot.appendChild(footer);

        adTrack.appendChild(slot);
    }

    pageNumber.textContent =
        "صفحة " + currentPage + " / " + (TOTAL_PAGES - 1);

    pageInfo.textContent =
        "الصفحة " + currentPage + " — الأماكن الإعلانية فارغة حتى إضافة الإعلانات.";

    adContainer.scrollLeft = 0;

    window.scrollTo(0, 0);
}

// الانتقال إلى الصفحة التالية مع العودة إلى البداية.
function nextPage() {
    currentPage = (currentPage + 1) % TOTAL_PAGES;
    renderPage();
}

// الانتقال إلى الصفحة السابقة مع العودة إلى النهاية.
function previousPage() {
    currentPage = (currentPage - 1 + TOTAL_PAGES) % TOTAL_PAGES;
    renderPage();
}

document.getElementById("nextPage").addEventListener("click", nextPage);
document.getElementById("prevPage").addEventListener("click", previousPage);

// سرعة التمرير العمودي: ضعف السرعة الأساسية المحددة.
let scrollingDirection = 0;
let animationFrame = null;
let lastTime = 0;

function scrollStep(timestamp) {
    if (!scrollingDirection) {
        animationFrame = null;
        lastTime = 0;
        return;
    }

    if (!lastTime) {
        lastTime = timestamp;
    }

    const delta = Math.min(timestamp - lastTime, 40);
    lastTime = timestamp;

    const speed = 1.2; // سرعة أساسية بالبكسل لكل ميلي ثانية
    window.scrollBy(0, scrollingDirection * speed * 2 * delta);

    animationFrame = requestAnimationFrame(scrollStep);
}

function startScrolling(direction) {
    scrollingDirection = direction;

    if (!animationFrame) {
        animationFrame = requestAnimationFrame(scrollStep);
    }
}

function stopScrolling() {
    scrollingDirection = 0;
}

const scrollUp = document.getElementById("scrollUp");
const scrollDown = document.getElementById("scrollDown");

scrollUp.addEventListener("pointerdown", () => startScrolling(-1));
scrollDown.addEventListener("pointerdown", () => startScrolling(1));

for (const button of [scrollUp, scrollDown]) {
    button.addEventListener("pointerup", stopScrolling);
    button.addEventListener("pointerleave", stopScrolling);
    button.addEventListener("pointercancel", stopScrolling);
}

document.addEventListener("visibilitychange", () => {
    if (document.hidden) {
        stopScrolling();
    }
});

// عرض الصفحة الأولى عند فتح الموقع.
renderPage();
</script>

</body>
</html>
