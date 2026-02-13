---
title: "地球毁灭后的365年"
date: 2026-02-13
categories: ["RECENTLY"]
draft: false
---

<p style="text-align: center; margin-top: 80px; font-family: serif;">
    这是一段关于记忆与净化的记录。
</p>

<button id="start-game" style="display:block; margin: 20px auto; padding: 12px 30px; cursor: pointer; border: 1px solid #dcdcdc; background: #fff; color: #333; transition: 0.3s;">开启观测</button>

<div id="game-overlay" style="display:none; opacity:0; position: fixed; top:0; left:0; width:100vw; height:100vh; background:#fff; z-index:9999; justify-content:center; align-items:center; cursor:crosshair; transition:opacity 1.5s ease;">
    <div id="stage" style="max-width:500px; width:80%; min-height:200px;"></div>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    const overlay = document.getElementById('game-overlay');
    const stage = document.getElementById('stage');
    const startBtn = document.getElementById('start-game');

    if (!overlay || !stage || !startBtn) return;

    const story = [
        { type: 'title', text: '1. 现实【愿你被世界簇拥，熠熠生辉】' },
        { type: 'shio', name: '汐', jp: 'ねえ、ハル。この街、綺麗だね。', text: '呐，悠。这座城市，挺漂亮的呢。' },
        { type: 'haru', name: '悠', jp: '……そうだね。', text: '……是啊。' },
        { type: 'mono', text: '（世界归于纯白。数据观测结束。）' },
        { type: 'title', text: 'END' }
    ];

    let index = 0;
    let isTransitioning = false;

    function advance() {
        if (isTransitioning) return;
        if (index >= story.length) {
            overlay.style.opacity = '0';
            setTimeout(() => {
                overlay.style.display = 'none';
                document.body.style.overflow = 'auto';
            }, 1500);
            return;
        }

        isTransitioning = true;
        overlay.style.display = 'flex';
        setTimeout(() => overlay.style.opacity = '1', 50);

        const data = story[index];
        stage.innerHTML = `<div style="font-family:'Hiragino Mincho ProN','Noto Serif SC',serif; letter-spacing:0.05em;">
            ${data.name ? `<span style="color:#999; font-size:11px; display:block; margin-bottom:8px;">${data.name}</span>` : ''}
            ${data.jp ? `<span style="color:#ccc; font-size:12px; display:block; margin-bottom:4px; font-style:italic;">${data.jp}</span>` : ''}
            <span style="color:${data.type==='mono'?'#ccc':'#1a1a1a'}; font-size:${data.type==='title'?'14px':'13px'}; line-height:2;">${data.text}</span>
        </div>`;
        index++;
        setTimeout(() => { isTransitioning = false; }, 400);
    }

    startBtn.addEventListener("click", function() {
        document.body.style.overflow = 'hidden';
        advance();
    });

    overlay.addEventListener("click", advance);
});
</script>
