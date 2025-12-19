# chenguoteng230-droid.github.io
物理3D实验室
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>演示文稿 - 2025/12/17</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        html, body {
            width: 100%;
            height: 100%;
            overflow: hidden;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'PingFang SC', 'Microsoft YaHei', sans-serif;
        }
        
        /* 主容器 - 黑色网格背景 */
        .presentation-container {
            width: 100vw;
            height: 100vh;
            display: flex;
            flex-direction: column;
            background-color: #0a0a0a;
            background-image: 
                linear-gradient(rgba(255, 255, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
            background-size: 20px 20px;
        }
        
        /* 顶部工具栏 */
        .top-bar {
            height: 48px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 20px;
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.08);
            flex-shrink: 0;
        }
        
        .top-bar-left, .top-bar-right {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .page-info {
            color: white;
            font-size: 14px;
            font-weight: 500;
        }
        
        .page-dots {
            display: flex;
            gap: 6px;
        }
        
        .page-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.3);
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .page-dot.active {
            background: white;
            transform: scale(1.2);
        }
        
        .page-dot:hover {
            background: rgba(255, 255, 255, 0.6);
        }
        
        .shortcuts {
            color: rgba(255, 255, 255, 0.5);
            font-size: 12px;
        }
        
        /* 幻灯片容器 */
        .slides-wrapper {
            flex: 1;
            position: relative;
            overflow: hidden;
        }
        
        .slides-track {
            display: flex;
            height: 100%;
            transition: transform 0.5s ease-in-out;
        }
        
        .slide {
            flex-shrink: 0;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 12px 72px;
        }
        
        .slide-frame {
            width: 100%;
            height: 100%;
            max-width: 100%;
            border: none;
            border-radius: 8px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6);
            background: white;
        }
        
        /* 导航热区 - 悬浮时显示按钮 */
        .nav-zone {
            position: absolute;
            top: 0;
            bottom: 0;
            width: 96px;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 100;
        }
        
        .nav-zone.prev { left: 0; }
        .nav-zone.next { right: 0; }
        
        .nav-btn {
            width: 56px;
            height: 56px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            background: rgba(0, 0, 0, 0.5);
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            opacity: 0;
        }
        
        .nav-zone:hover .nav-btn {
            opacity: 1;
        }
        
        .nav-btn:hover {
            background: rgba(0, 0, 0, 0.7);
            transform: scale(1.1);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.4);
        }
        
        .nav-btn:disabled {
            visibility: hidden;
        }
        
        .nav-zone:has(.nav-btn:disabled) {
            pointer-events: none;
        }
        
        .nav-btn svg {
            width: 28px;
            height: 28px;
        }
    </style>
</head>
<body>
    <div class="presentation-container">
        <!-- 顶部工具栏 -->
        <div class="top-bar">
            <div class="top-bar-left">
                <span class="page-info"><span id="currentPage">1</span> / 1</span>
                <div class="page-dots" id="pageDots">
                    <span class="page-dot active" data-index="0"></span>
                </div>
            </div>
            <div class="top-bar-right">
                <span class="shortcuts">← → 切换页面 | ESC 退出</span>
            </div>
        </div>
        
        <!-- 幻灯片区域 -->
        <div class="slides-wrapper">
            <div class="slides-track" id="slidesTrack">
                
                <div class="slide">
                    <iframe 
                        class="slide-frame"
                        srcdoc="<!DOCTYPE html>
<html lang=&quot;zh-CN&quot;>
<head>
    <meta charset=&quot;UTF-8&quot;>
    <title>物理实验：平面镜成像与重影效应</title>
    <style>
        /* --- 界面样式 (UI Style) --- */
        body { margin: 0; overflow: hidden; background-color: #0d0d0d; font-family: 'Segoe UI', sans-serif; }
        
        /* 控制面板容器 */
        #ui-panel {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 340px;
            background: rgba(25, 25, 30, 0.85); /* 深色磨砂背景 */
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            color: #eee;
            user-select: none;
            max-height: 90vh;
            overflow-y: auto;
        }
        /* 隐藏滚动条 */
        #ui-panel::-webkit-scrollbar { width: 0; }

        h2 { margin: 0 0 15px 0; font-size: 18px; color: #4db8ff; border-bottom: 1px solid rgba(255,255,255,0.15); padding-bottom: 10px; }
        h3 { margin: 15px 0 8px 0; font-size: 13px; color: #ffcc00; text-transform: uppercase; letter-spacing: 1px; }

        /* 滑块组 */
        .control-group { margin-bottom: 12px; }
        .label-row { display: flex; justify-content: space-between; font-size: 13px; color: #aaa; margin-bottom: 5px; }
        .val-text { font-family: 'Consolas', monospace; color: #fff; font-weight: bold; }

        /* 自定义滑块 */
        input[type=range] { -webkit-appearance: none; width: 100%; background: transparent; }
        input[type=range]:focus { outline: none; }
        input[type=range]::-webkit-slider-runnable-track { width: 100%; height: 4px; background: rgba(255,255,255,0.2); border-radius: 2px; }
        input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; height: 14px; width: 14px; border-radius: 50%; background: #fff; margin-top: -5px; box-shadow: 0 0 5px rgba(0,0,0,0.5); cursor: pointer; transition: 0.1s; }
        input[type=range]:active::-webkit-slider-thumb { transform: scale(1.3); background: #4db8ff; }

        /* 开关 */
        .toggle-row { display: flex; align-items: center; justify-content: space-between; margin-top: 15px; cursor: pointer; }
        .toggle-bg { width: 40px; height: 20px; background: #444; border-radius: 10px; position: relative; transition: 0.3s; }
        .toggle-dot { position: absolute; left: 2px; top: 2px; width: 16px; height: 16px; background: #fff; border-radius: 50%; transition: 0.3s; }
        input[type=checkbox] { display: none; }
        input[type=checkbox]:checked + .toggle-bg { background: #4db8ff; }
        input[type=checkbox]:checked + .toggle-bg .toggle-dot { left: 22px; }

        /* 按钮 */
        #reset-btn { width: 100%; padding: 10px; margin-top: 20px; background: rgba(255,255,255,0.1); border: 1px solid #555; color: #fff; border-radius: 6px; cursor: pointer; transition: 0.2s; }
        #reset-btn:hover { background: #4db8ff; border-color: #4db8ff; }

        /* 视角提示 */
        #fov-tip { position: absolute; top: 20px; left: 20px; color: rgba(255,255,255,0.5); font-size: 12px; pointer-events: none; }
        .vis-ok { color: #2ecc71; font-weight: bold; }
        .vis-no { color: #e74c3c; font-weight: bold; }
    </style>

    <!-- Three.js 核心库引入 -->
    <script async src=&quot;https://unpkg.com/es-module-shims@1.6.3/dist/es-module-shims.js&quot;></script>
    <script type=&quot;importmap&quot;>
      {
        &quot;imports&quot;: {
          &quot;three&quot;: &quot;https://unpkg.com/three@0.150.0/build/three.module.js&quot;,
          &quot;three/addons/&quot;: &quot;https://unpkg.com/three@0.150.0/examples/jsm/&quot;
        }
      }
    </script>
</head>
<body>

    <!-- 视角状态提示 -->
    <div id=&quot;fov-tip&quot;>
        观察状态: <span id=&quot;fov-status&quot; class=&quot;vis-ok&quot;>可见区域</span><br>
        <span style=&quot;font-size:10px&quot;>(仅在镜面前方 ±45° 可见像)</span>
    </div>

    <!-- 控制面板 -->
    <div id=&quot;ui-panel&quot;>
        <h2>平面镜成像实验室</h2>

        <h3>1. 蜡烛A (Object)</h3>
        <div class=&quot;control-group&quot;>
            <div class=&quot;label-row&quot;><span>物距 (u)</span><span id=&quot;txt-u&quot; class=&quot;val-text&quot;>15.0 cm</span></div>
            <input type=&quot;range&quot; id=&quot;inp-u&quot; min=&quot;5&quot; max=&quot;40&quot; step=&quot;0.5&quot; value=&quot;15&quot;>
        </div>
        <div class=&quot;control-group&quot;>
            <div class=&quot;label-row&quot;><span>左右偏移</span><span id=&quot;txt-off&quot; class=&quot;val-text&quot;>0.0 cm</span></div>
            <input type=&quot;range&quot; id=&quot;inp-off&quot; min=&quot;-15&quot; max=&quot;15&quot; step=&quot;0.5&quot; value=&quot;0&quot;>
        </div>

        <h3>2. 玻璃板 (Glass)</h3>
        <div class=&quot;control-group&quot;>
            <div class=&quot;label-row&quot;><span>倾斜角度</span><span id=&quot;txt-tilt&quot; class=&quot;val-text&quot;>0.0°</span></div>
            <input type=&quot;range&quot; id=&quot;inp-tilt&quot; min=&quot;-10&quot; max=&quot;10&quot; step=&quot;0.5&quot; value=&quot;0&quot;>
        </div>
        <div class=&quot;control-group&quot;>
            <div class=&quot;label-row&quot;><span style=&quot;color:#ffaaaa&quot;>玻璃厚度 (重影)</span><span id=&quot;txt-thick&quot; class=&quot;val-text&quot; style=&quot;color:#ffaaaa&quot;>0.2 cm</span></div>
            <input type=&quot;range&quot; id=&quot;inp-thick&quot; min=&quot;0&quot; max=&quot;1.0&quot; step=&quot;0.1&quot; value=&quot;0.2&quot;>
        </div>

        <h3>3. 蜡烛B (Tool)</h3>
        <div class=&quot;control-group&quot;>
            <div class=&quot;label-row&quot;><span>B到镜面距离</span><span id=&quot;txt-ub&quot; class=&quot;val-text&quot;>20.0 cm</span></div>
            <input type=&quot;range&quot; id=&quot;inp-ub&quot; min=&quot;5&quot; max=&quot;45&quot; step=&quot;0.1&quot; value=&quot;20&quot;>
        </div>
        
        <label class=&quot;toggle-row&quot;>
            <span>显示垂直标尺 (Y轴)</span>
            <input type=&quot;checkbox&quot; id=&quot;chk-ruler&quot;>
            <div class=&quot;toggle-bg&quot;><div class=&quot;toggle-dot&quot;></div></div>
        </label>

        <button id=&quot;reset-btn&quot;>重置实验</button>
    </div>

    <script type=&quot;module&quot;>
        import * as THREE from 'three';
        import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

        // --- 1. 场景初始化 ---
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0x121215); // 暗室背景
        scene.fog = new THREE.Fog(0x121215, 20, 120);

        const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 500);
        camera.position.set(0, 25, 50);

        const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.shadowMap.enabled = true;
        renderer.shadowMap.type = THREE.PCFSoftShadowMap;
        document.body.appendChild(renderer.domElement);

        // 灯光系统
        scene.add(new THREE.AmbientLight(0x404040, 1.2)); // 环境光
        
        const spotLight = new THREE.SpotLight(0xffffff, 1.0);
        spotLight.position.set(0, 50, 20);
        spotLight.angle = 0.6;
        spotLight.penumbra = 0.5;
        spotLight.castShadow = true;
        scene.add(spotLight);

        // --- 2. 基础环境 ---
        // 桌面方格
        const gridHelper = new THREE.GridHelper(100, 100, 0x555555, 0x222222);
        scene.add(gridHelper);

        const plane = new THREE.Mesh(
            new THREE.PlaneGeometry(200, 200),
            new THREE.MeshLambertMaterial({ color: 0x181818 })
        );
        plane.rotation.x = -Math.PI / 2;
        plane.position.y = -0.01;
        plane.receiveShadow = true;
        scene.add(plane);

        // --- 3. 高级模型构建 ---

        // 3.1 动态标尺 (Canvas Texture)
        function createRuler() {
            const canvas = document.createElement('canvas');
            canvas.width = 128; canvas.height = 1024;
            const ctx = canvas.getContext('2d');
            
            // 背景透明
            ctx.clearRect(0,0,128,1024);
            
            // 绘制刻度
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 40px Arial';
            ctx.textAlign = 'right';
            ctx.textBaseline = 'middle';
            
            const totalCm = 20; 
            const pxPerCm = 1024 / totalCm;

            // 边框线
            ctx.fillStyle = 'rgba(255,255,255,0.2)';
            ctx.fillRect(0,0,128,1024);

            ctx.fillStyle = '#ffffff';
            for(let i=0; i<=totalCm; i++) {
                const y = 1024 - (i * pxPerCm);
                // 长刻度
                ctx.fillRect(0, y-2, 50, 4);
                // 数字 (每5cm)
                if(i % 5 === 0) ctx.fillText(i, 110, y);
                // 短刻度
                for(let j=1; j<5; j++) {
                    const sy = y - (j * pxPerCm/5);
                    ctx.fillRect(0, sy-1, 25, 2);
                }
            }

            const tex = new THREE.CanvasTexture(canvas);
            // 使用 PlaneGeometry 避免侧面拉伸
            const geo = new THREE.PlaneGeometry(5, 20); 
            const mat = new THREE.MeshBasicMaterial({ 
                map: tex, 
                transparent: true, 
                opacity: 0.9, 
                side: THREE.DoubleSide,
                depthWrite: false 
            });
            const mesh = new THREE.Mesh(geo, mat);
            mesh.position.set(-18, 10, 0); // 放在左侧
            mesh.visible = false;
            return mesh;
        }
        const ruler = createRuler();
        scene.add(ruler);

        // 3.2 玻璃板 (Glass)
        const mirrorGroup = new THREE.Group();
        const glassGeo = new THREE.BoxGeometry(30, 20, 1); // 基础厚度1
        const glassMat = new THREE.MeshPhysicalMaterial({
            color: 0x88ccff,
            metalness: 0.1, roughness: 0.05,
            transmission: 0.9, transparent: true, opacity: 0.4,
            side: THREE.DoubleSide,
            depthWrite: false // 关键：不遮挡背后的虚像
        });
        const glass = new THREE.Mesh(glassGeo, glassMat);
        glass.position.y = 10;
        glass.renderOrder = 10; // 玻璃最后渲染
        mirrorGroup.add(glass);
        
        const base = new THREE.Mesh(
            new THREE.BoxGeometry(32, 0.5, 4),
            new THREE.MeshStandardMaterial({ color: 0x333333 })
        );
        base.position.y = 0.25;
        mirrorGroup.add(base);
        scene.add(mirrorGroup);

        // 3.3 真实火焰 (LatheGeometry)
        function createFlameMesh(scale, color, opacity) {
            // 生成水滴状轮廓点
            const points = [];
            for ( let i = 0; i <= 20; i ++ ) {
                const t = i / 20; 
                // 形状公式：sin(t*PI) 制造弧度，(1-t*0.6) 让顶部变尖
                const x = Math.sin(t * Math.PI) * 0.4 * (1 - t * 0.6) * scale;
                const y = t * 1.5 * scale;
                points.push( new THREE.Vector2( x, y ) );
            }
            const geo = new THREE.LatheGeometry( points, 16 );
            const mat = new THREE.MeshBasicMaterial({ 
                color: color, transparent: true, opacity: opacity, depthWrite: false, side: THREE.DoubleSide
            });
            return new THREE.Mesh(geo, mat);
        }

        function createComplexFlame() {
            const g = new THREE.Group();
            // 1. 外焰 (大，淡黄)
            const out = createFlameMesh(1.0, 0xffaa33, 0.3);
            out.name = 'f_out';
            g.add(out);
            // 2. 内焰 (中，橙红)
            const mid = createFlameMesh(0.7, 0xff4400, 0.6);
            mid.name = 'f_mid';
            g.add(mid);
            // 3. 焰心 (小，蓝)
            const core = createFlameMesh(0.3, 0x0033ff, 0.8);
            core.name = 'f_core';
            g.add(core);
            return g;
        }

        // 3.4 蜡烛工厂
        function createCandle(type) {
            // type: REAL, GHOST_1, GHOST_2, TOOL
            const g = new THREE.Group();
            const isGhost = (type === 'GHOST_1' || type === 'GHOST_2');
            const isLit = (type !== 'TOOL');

            // 蜡体
            const waxMat = new THREE.MeshStandardMaterial({ 
                color: 0xff3333,
                transparent: isGhost,
                opacity: isGhost ? (type==='GHOST_2' ? 0.2 : 0.45) : 1.0, // 第二虚像更淡
                depthWrite: !isGhost
            });
            const wax = new THREE.Mesh(new THREE.CylinderGeometry(0.7, 0.7, 6, 32), waxMat);
            wax.position.y = 3;
            if(!isGhost) wax.castShadow = true;
            g.add(wax);

            // 烛芯
            const wick = new THREE.Mesh(new THREE.CylinderGeometry(0.06, 0.06, 0.5), new THREE.MeshBasicMaterial({color:0x111111}));
            wick.position.y = 6.2;
            g.add(wick);

            // 火焰
            if(isLit) {
                const flame = createComplexFlame();
                flame.position.y = 6.4;
                flame.name = &quot;flame_grp&quot;;
                g.add(flame);

                // 只有实物有光源
                if(type === 'REAL') {
                    const l = new THREE.PointLight(0xffaa00, 1.5, 12);
                    l.position.set(0, 7, 0);
                    g.add(l);
                }
            }

            // 渲染顺序：虚像(0) -> 实物(1) -> 玻璃(10)
            g.renderOrder = isGhost ? 0 : 1;
            return g;
        }

        const candleA = createCandle('REAL');
        scene.add(candleA);

        const image1 = createCandle('GHOST_1'); // 主像
        scene.add(image1);

        const image2 = createCandle('GHOST_2'); // 重影
        scene.add(image2);

        const candleB = createCandle('TOOL'); // 工具B
        scene.add(candleB);


        // --- 4. 交互逻辑 ---
        
        // UI 绑定
        const ui = {
            u: document.getElementById('inp-u'),
            off: document.getElementById('inp-off'),
            tilt: document.getElementById('inp-tilt'),
            thick: document.getElementById('inp-thick'),
            ub: document.getElementById('inp-ub'),
            ruler: document.getElementById('chk-ruler'),
            
            txt_u: document.getElementById('txt-u'),
            txt_off: document.getElementById('txt-off'),
            txt_tilt: document.getElementById('txt-tilt'),
            txt_thick: document.getElementById('txt-thick'),
            txt_ub: document.getElementById('txt-ub'),
            
            fov: document.getElementById('fov-status')
        };

        function update() {
            const u = parseFloat(ui.u.value);
            const off = parseFloat(ui.off.value);
            const tilt = parseFloat(ui.tilt.value);
            const thick = parseFloat(ui.thick.value);
            const ub = parseFloat(ui.ub.value);

            // 文本更新
            ui.txt_u.innerText = u.toFixed(1) + &quot; cm&quot;;
            ui.txt_off.innerText = off.toFixed(1) + &quot; cm&quot;;
            ui.txt_tilt.innerText = tilt.toFixed(1) + &quot;°&quot;;
            ui.txt_thick.innerText = thick.toFixed(1) + &quot; cm&quot;;
            ui.txt_ub.innerText = ub.toFixed(1) + &quot; cm&quot;;

            // 1. 标尺开关
            ruler.visible = ui.ruler.checked;

            // 2. 玻璃厚度 (Scale Z)
            // 视觉上最少保留0.05厚度，否则模型消失
            const visThick = Math.max(0.05, thick);
            glass.scale.z = visThick; 

            // 3. 蜡烛A 位置
            candleA.position.set(off, 0, u);

            // 4. 镜子旋转
            const rad = THREE.MathUtils.degToRad(tilt);
            mirrorGroup.rotation.x = rad;

            // 5. 计算主虚像 (Image 1)
            // 假设前表面在逻辑零点
            const normal = new THREE.Vector3(0, 0, 1).applyAxisAngle(new THREE.Vector3(1, 0, 0), rad);
            const planeMath = new THREE.Plane(normal, 0);
            
            const objPos = candleA.position.clone();
            const d = planeMath.distanceToPoint(objPos);
            // 镜像公式 P' = P - 2dN
            const img1Pos = objPos.clone().sub(normal.clone().multiplyScalar(2 * d));
            
            image1.position.copy(img1Pos);
            image1.rotation.x = rad * 2;

            // 6. 计算重影 (Image 2 - 后表面反射)
            // 物理近似：重影会比主像“深”一个厚度相关的距离
            if(thick < 0.1) {
                image2.visible = false;
            } else {
                image2.visible = true;
                // 沿法线向后偏移 (thick * 1.5 是经验视觉系数，模拟折射路径)
                const offset = normal.clone().multiplyScalar(-thick * 1.5);
                image2.position.copy(img1Pos).add(offset);
                image2.rotation.x = rad * 2;
            }

            // 7. 蜡烛B 位置
            // B在镜后，Z为负。我们让B的X跟随A的偏移(简化操作)，只调节距离
            candleB.position.set(off, 0, -ub);
        }

        // 事件监听
        ['input', 'change'].forEach(evt => {
            [ui.u, ui.off, ui.tilt, ui.thick, ui.ub, ui.ruler].forEach(el => el.addEventListener(evt, update));
        });

        document.getElementById('reset-btn').onclick = () => {
            ui.u.value = 15; ui.off.value = 0; ui.tilt.value = 0; 
            ui.thick.value = 0.2; ui.ub.value = 20; ui.ruler.checked = false;
            update();
        };

        // --- 5. 动画循环 ---
        const clock = new THREE.Clock();
        const controls = new OrbitControls(camera, renderer.domElement);
        controls.enableDamping = true;

        function animate() {
            requestAnimationFrame(animate);
            const t = clock.getElapsedTime();

            // 火焰律动 (针对所有点燃的蜡烛)
            [candleA, image1, image2].forEach(c => {
                const grp = c.getObjectByName(&quot;flame_grp&quot;);
                if(grp) {
                    // 外焰呼吸
                    const out = grp.getObjectByName('f_out');
                    const s1 = 1 + Math.sin(t * 8) * 0.05;
                    out.scale.set(s1, s1, s1);
                    out.rotation.y = t * 0.2;
                    
                    // 内焰微动
                    const mid = grp.getObjectByName('f_mid');
                    mid.scale.setScalar(1 + Math.cos(t * 10) * 0.03);
                    
                    // 焰心颤动
                    const core = grp.getObjectByName('f_core');
                    core.scale.setScalar(1 + Math.sin(t * 15) * 0.02);
                }
            });

            // 视场角逻辑 (Field of View)
            const angleRad = Math.atan2(camera.position.x, camera.position.z);
            const angleDeg = THREE.MathUtils.radToDeg(angleRad);
            const isFront = camera.position.z > 0;
            const inFOV = Math.abs(angleDeg) <= 45;

            // 控制虚像可见性
            const visible = isFront && inFOV;
            image1.visible = visible;
            // image2 还要看厚度
            if(visible && parseFloat(ui.thick.value) >= 0.1) {
                image2.visible = true;
            } else {
                image2.visible = false;
            }

            // UI 状态提示
            if(visible) {
                ui.fov.innerText = &quot;可见区域&quot;;
                ui.fov.className = &quot;vis-ok&quot;;
            } else {
                ui.fov.innerText = &quot;不可见 (超出视角)&quot;;
                ui.fov.className = &quot;vis-no&quot;;
            }

            controls.update();
            renderer.render(scene, camera);
        }

        // 初始化
        update();
        animate();

        // 窗口自适应
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

    </script>
</body>
</html>

"
                        title="物理实验：平面镜成像与重影效应"
                    ></iframe>
                </div>
                
            </div>
            
            <!-- 导航热区 - 悬浮显示按钮 -->
            <div class="nav-zone prev">
                <button class="nav-btn" id="prevBtn">
                    <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
                    </svg>
                </button>
            </div>
            <div class="nav-zone next">
                <button class="nav-btn" id="nextBtn">
                    <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
                    </svg>
                </button>
            </div>
        </div>
    </div>
    
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const slides = document.querySelectorAll('.slide');
            const track = document.getElementById('slidesTrack');
            const prevBtn = document.getElementById('prevBtn');
            const nextBtn = document.getElementById('nextBtn');
            const currentPageEl = document.getElementById('currentPage');
            const dots = document.querySelectorAll('.page-dot');
            
            let currentIndex = 0;
            const totalSlides = slides.length;
            
            function updateSlide() {
                track.style.transform = `translateX(-${currentIndex * 100}%)`;
                currentPageEl.textContent = currentIndex + 1;
                
                // 更新导航按钮状态
                prevBtn.disabled = currentIndex === 0;
                nextBtn.disabled = currentIndex === totalSlides - 1;
                
                // 更新页面指示点
                dots.forEach((dot, i) => {
                    dot.classList.toggle('active', i === currentIndex);
                });
            }
            
            function goToSlide(index) {
                if (index >= 0 && index < totalSlides) {
                    currentIndex = index;
                    updateSlide();
                }
            }
            
            // 按钮事件
            prevBtn.addEventListener('click', () => goToSlide(currentIndex - 1));
            nextBtn.addEventListener('click', () => goToSlide(currentIndex + 1));
            
            // 点击页面指示点
            dots.forEach((dot, i) => {
                dot.addEventListener('click', () => goToSlide(i));
            });
            
            // 键盘导航
            document.addEventListener('keydown', (e) => {
                if (e.key === 'ArrowLeft') goToSlide(currentIndex - 1);
                if (e.key === 'ArrowRight') goToSlide(currentIndex + 1);
                if (e.key === 'Home') goToSlide(0);
                if (e.key === 'End') goToSlide(totalSlides - 1);
            });
            
            // 初始化
            updateSlide();
        });
    </script>
</body>
</html>
