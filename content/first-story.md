---
title: "地球毁灭后的365年"
date: 2026-02-13T12:00:00+08:00
categories: ["recently"]
draft: false
---

<div id="game-trigger" style="text-align: center; margin-top: 80px; font-family: serif;">
    <p style="color: #666; letter-spacing: 2px;">这是一段关于记忆与净化的记录。</p>
    <button onclick="startGame()" style="margin-top: 20px; padding: 12px 30px; cursor: pointer; border: 1px solid #dcdcdc; background: #fff; color: #333; transition: 0.3s; letter-spacing: 1px;">开启观测</button>
</div>

<div id="game-overlay" style="display:none; opacity: 0; position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: #fff; z-index: 9999; justify-content: center; align-items: center; cursor: crosshair; transition: opacity 1.5s ease;">
    <div id="stage" style="max-width: 500px; width: 80%; min-height: 200px;"></div>
</div>

<script>
// 修正了逗号和逻辑的剧本数组
const story = [
    { type: 'title', text: '1. 现实【愿你被世界簇拥，熠熠生辉】' },
    { type: 'shio', name: '汐', jp: 'ねえ、ハル。この街、綺麗だね。', text: '呐，悠。这座城市，挺漂亮的呢。' },
    { type: 'haru', name: '悠', jp: '……そうだね。', text: '……是啊。' },
    { type: 'shio', name: '汐', jp: '私の顔、ちゃんと見えてる？', text: '我的脸，能好好看清吗？' },
    { type: 'haru', name: '悠', jp: '……毎日見てる。', text: '……每天都在看。' },
    { type: 'shio', name: '汐', jp: '君が見てるのは‘検体’としての私。', text: '你看的是作为“检体”的我。' },
    { type: 'shio', name: '汐', jp: '……ハル、今の私の瞳、何色に見える？', text: '……悠，我现在的瞳孔，在你看来是什么颜色？' },
    { type: 'haru', name: '悠', jp: '……濁った、灰色だ。', text: '……浑浊的，灰色。' },
    { type: 'shio', name: '汐', jp: '私はここにいるよ。', text: '我就在这里哦。' },
    { type: 'shio', name: '汐', jp: '君が歩く道のそばに、名前も知らない花として咲いているから。', text: '会在你行走的路旁，作为一朵无名的花盛开着。' },
    { type: 'mono', text: '（世界归于纯白。数据观测结束。）' },
    { type: 'mono', text: '（点击继续...）' },
    { type: 'title', text: 'END' }
];

let index = 0;
let isTransitioning = false;

function startGame() {
    const overlay = document.getElementById('game-overlay');
    overlay.style.display = 'flex';
    // 强制重绘以触发 transition
    setTimeout(() => { overlay.style.opacity = '1'; }, 50);
    document.body.style.overflow = 'hidden';
    advance();
}

function advance() {
    if (isTransitioning) return;
    const stage = document.getElementById('stage');
    
    if (index >= story.length) {
        document.getElementById('game-overlay').style.opacity = '0';
        setTimeout(() => { 
            document.body.style.overflow = 'auto';
            location.reload(); 
        }, 1500);
        return;
    }

    isTransitioning = true;
    const data = story[index];

    // 文字切换的淡入淡出节奏
    stage.style.transition = "opacity 0.6s ease";
    stage.style.opacity = "0";

    setTimeout(() => {
        let content = `<div style="font-family: 'Hiragino Mincho ProN', 'Noto Serif SC', serif; letter-spacing: 0.05em;">`;
        
        if (data.name) {
            content += `<span style="color:#999; font-size:11px; display:block; margin-bottom: 8px; letter-spacing: 2px;">${data.name}</span>`;
        }
        
        if (data.jp) {
            content += `<span style="color:#ccc; font-size:12px; display:block; margin-bottom: 4px; font-style: italic;">${data.jp}</span>`;
        }
        
        const textColor = data.type === 'mono' ? '#ccc' : '#1a1a1a';
        const fontSize = data.type === 'title' ? '14px' : '13px';
        
        content += `<span style="color:${textColor}; font-size:${fontSize}; line-height: 2;">${data.text}</span>`;
        content += `</div>`;
        
        stage.innerHTML = content;
        stage.style.opacity = "1";
        
        index++;
        setTimeout(() => { isTransitioning = false; }, 400);
    }, 600);
}

// 绑定全屏层点击事件
document.getElementById('game-overlay').onclick = advance;
</script>
