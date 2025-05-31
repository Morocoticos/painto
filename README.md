

<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>painto wed</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/spectrum-colorpicker2/dist/spectrum.min.css">
    <style id="app-style">
        :root {
            --primary-color: #4a86e8;
            --secondary-color: #f7cb4d;
            --dark-color: #333;
            --light-color: #f8f9fa;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f0f2f5;
            overflow-x: hidden;
            height: 100vh;
            margin: 0;
            padding: 0;
        }
        
        .app-container {
            max-width: 1600px;
            margin: 0 auto;
            padding: 20px;
            height: calc(100vh - 40px);
            display: flex;
            flex-direction: column;
        }
        
        .app-header {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .app-header h1 {
            color: var(--primary-color);
            font-weight: 700;
            font-size: 2.5rem;
            margin: 0;
            text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.1);
        }
        
        .canvas-container {
            display: flex;
            flex: 1;
            background-color: white;
            border-radius: 12px;
            box-shadow: 0 6px 24px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            position: relative;
        }
        
        .toolbar {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            padding: 15px;
            background-color: #fff;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
            margin-bottom: 15px;
            justify-content: center;
        }
        
        .tool-btn {
            width: 50px;
            height: 50px;
            border-radius: 10px;
            border: none;
            background-color: var(--light-color);
            color: var(--dark-color);
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .tool-btn:hover {
            background-color: var(--secondary-color);
            transform: translateY(-2px);
        }
        
        .tool-btn.active {
            background-color: var(--primary-color);
            color: white;
        }
        
        .main-area {
            display: flex;
            flex: 1;
        }
        
        .canvas-wrapper {
            flex: 1;
            position: relative;
            background-color: #f9f9f9;
            background-image: 
                linear-gradient(45deg, #e0e0e0 25%, transparent 25%), 
                linear-gradient(-45deg, #e0e0e0 25%, transparent 25%), 
                linear-gradient(45deg, transparent 75%, #e0e0e0 75%), 
                linear-gradient(-45deg, transparent 75%, #e0e0e0 75%);
            background-size: 20px 20px;
            background-position: 0 0, 0 10px, 10px -10px, -10px 0px;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        
        #canvas {
            background-color: white;
            cursor: crosshair;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            touch-action: none;
        }
        
        .color-palette {
            display: flex;
            gap: 10px;
            padding: 15px;
            background-color: #fff;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
            margin-bottom: 15px;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .color-swatch {
            width: 40px;
            height: 40px;
            border-radius: 8px;
            cursor: pointer;
            transition: transform 0.2s ease;
            border: 3px solid transparent;
        }
        
        .color-swatch:hover {
            transform: scale(1.1);
        }
        
        .color-swatch.active {
            border: 3px solid var(--dark-color);
            transform: scale(1.1);
        }
        
        .add-color-btn {
            width: 40px;
            height: 40px;
            border-radius: 8px;
            background-color: #f8f9fa;
            border: 2px dashed #ccc;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            color: #888;
            transition: all 0.3s ease;
        }
        
        .add-color-btn:hover {
            background-color: #e9ecef;
            color: var(--dark-color);
        }
        
        .side-panel {
            width: 250px;
            background-color: white;
            padding: 20px;
            border-left: 1px solid #eee;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .panel-section {
            background-color: #f8f9fa;
            border-radius: 10px;
            padding: 15px;
        }
        
        .panel-section h3 {
            font-size: 1rem;
            margin-top: 0;
            margin-bottom: 15px;
            color: var(--dark-color);
            font-weight: 600;
        }
        
        .slider-container {
            margin-bottom: 15px;
        }
        
        .slider-container label {
            display: block;
            margin-bottom: 5px;
            font-size: 0.85rem;
            color: #666;
        }
        
        .slider-container input[type="range"] {
            width: 100%;
            margin: 0;
            accent-color: var(--primary-color);
        }
        
        .slider-value {
            margin-top: 5px;
            font-size: 0.8rem;
            text-align: right;
            color: #666;
        }
        
        .action-buttons {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }
        
        .btn-action {
            flex: 1;
            padding: 10px;
            border: none;
            border-radius: 8px;
            background-color: var(--light-color);
            color: var(--dark-color);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .btn-action:hover {
            background-color: #e2e6ea;
        }
        
        .btn-action i {
            margin-right: 5px;
        }
        
        .btn-save {
            background-color: var(--primary-color);
            color: white;
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-top: auto;
        }
        
        .btn-save:hover {
            background-color: #3a76d8;
            transform: translateY(-2px);
        }
        
        .auto-save-toggle {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-top: 15px;
            padding: 10px;
            background-color: #f8f9fa;
            border-radius: 8px;
        }
        
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 46px;
            height: 24px;
        }
        
        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }
        
        .toggle-slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 24px;
        }
        
        .toggle-slider:before {
            position: absolute;
            content: "";
            height: 18px;
            width: 18px;
            left: 3px;
            bottom: 3px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }
        
        input:checked + .toggle-slider {
            background-color: var(--primary-color);
        }
        
        input:checked + .toggle-slider:before {
            transform: translateX(22px);
        }
        
        .loading-spinner {
            border: 3px solid #f3f3f3;
            border-top: 3px solid var(--primary-color);
            border-radius: 50%;
            width: 20px;
            height: 20px;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .feedback-msg {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            padding: 15px 25px;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            border-radius: 8px;
            z-index: 1000;
            opacity: 0;
            transition: opacity 0.3s ease;
            font-weight: 500;
            pointer-events: none;
        }
        
        .feedback-msg.show {
            opacity: 1;
        }
        
        .restore-dialog {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        
        .restore-dialog-content {
            background-color: white;
            border-radius: 12px;
            padding: 30px;
            max-width: 400px;
            width: 100%;
            text-align: center;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }
        
        .restore-dialog-content h2 {
            margin-top: 0;
            color: var(--primary-color);
            font-size: 1.5rem;
        }
        
        .restore-dialog-content p {
            margin: 20px 0;
            color: #555;
        }
        
        .restore-dialog-buttons {
            display: flex;
            gap: 15px;
            justify-content: center;
        }
        
        .restore-dialog-buttons button {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .btn-restore {
            background-color: var(--primary-color);
            color: white;
        }
        
        .btn-restore:hover {
            background-color: #3a76d8;
        }
        
        .btn-new {
            background-color: #e9ecef;
            color: #555;
        }
        
        .btn-new:hover {
            background-color: #dde2e6;
        }
        
        .color-picker-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        
        .color-picker-content {
            background-color: white;
            border-radius: 12px;
            padding: 25px;
            max-width: 350px;
            width: 100%;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }
        
        .color-picker-content h3 {
            margin-top: 0;
            margin-bottom: 20px;
            color: var(--primary-color);
        }
        
        .color-picker-buttons {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
            margin-top: 20px;
        }
        
        .color-picker-buttons button {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .btn-cancel {
            background-color: #e9ecef;
            color: #555;
        }
        
        .btn-add-color {
            background-color: var(--primary-color);
            color: white;
        }
        
        /* Responsive adjustments */
        @media (max-width: 992px) {
            .main-area {
                flex-direction: column;
            }
            
            .side-panel {
                width: 100%;
                border-left: none;
                border-top: 1px solid #eee;
            }
        }
        
        @media (max-width: 768px) {
            .app-container {
                padding: 10px;
                height: calc(100vh - 20px);
            }
            
            .tool-btn {
                width: 40px;
                height: 40px;
            }
            
            .color-swatch {
                width: 30px;
                height: 30px;
            }
        }
        
        @media (max-width: 576px) {
            .app-header h1 {
                font-size: 1.8rem;
            }
            
            .toolbar, .color-palette {
                padding: 10px;
                gap: 5px;
            }
            
            .tool-btn {
                width: 36px;
                height: 36px;
                font-size: 1rem;
            }
        }
        
        /* Canvas Loading Animation */
        .canvas-loading {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(255, 255, 255, 0.8);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 100;
        }
        
        .canvas-loading .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid #f3f3f3;
            border-top: 5px solid var(--primary-color);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-bottom: 15px;
        }
        
        .canvas-loading p {
            color: var(--primary-color);
            font-weight: 600;
        }
    </style>
</head>

<body>
    <div class="app-container">
        <div class="app-header">
            <h1><i class="fas fa-paint-brush"></i> Canvas Creations</h1>
        </div>
        
        <div class="toolbar">
            <button class="tool-btn active" id="brush-tool" title="Brush">
                <i class="fas fa-paint-brush"></i>
            </button>
            <button class="tool-btn" id="pencil-tool" title="Pencil">
                <i class="fas fa-pencil-alt"></i>
            </button>
            <button class="tool-btn" id="eraser-tool" title="Eraser">
                <i class="fas fa-eraser"></i>
            </button>
            <button class="tool-btn" id="fill-tool" title="Fill Bucket">
                <i class="fas fa-fill-drip"></i>
            </button>
            <button class="tool-btn" id="eyedropper-tool" title="Color Picker">
                <i class="fas fa-eye-dropper"></i>
            </button>
        </div>
        
        <div class="color-palette">
            <div class="color-swatch active" style="background-color: #000000;" data-color="#000000"></div>
            <div class="color-swatch" style="background-color: #ff0000;" data-color="#ff0000"></div>
            <div class="color-swatch" style="background-color: #ff9900;" data-color="#ff9900"></div>
            <div class="color-swatch" style="background-color: #ffff00;" data-color="#ffff00"></div>
            <div class="color-swatch" style="background-color: #00ff00;" data-color="#00ff00"></div>
            <div class="color-swatch" style="background-color: #00ffff;" data-color="#00ffff"></div>
            <div class="color-swatch" style="background-color: #0000ff;" data-color="#0000ff"></div>
            <div class="color-swatch" style="background-color: #9900ff;" data-color="#9900ff"></div>
            <div class="color-swatch" style="background-color: #ff00ff;" data-color="#ff00ff"></div>
            <div class="color-swatch" style="background-color: #ffffff;" data-color="#ffffff"></div>
            <div class="add-color-btn" id="add-color-btn">
                <i class="fas fa-plus"></i>
            </div>
        </div>
        
        <div class="main-area">
            <div class="canvas-wrapper">
                <canvas id="canvas"></canvas>
                <div class="canvas-loading" id="canvas-loading">
                    <div class="spinner"></div>
                    <p>Loading canvas...</p>
                </div>
            </div>
            
            <div class="side-panel">
                <div class="panel-section">
                    <h3>Brush Settings</h3>
                    <div class="slider-container">
                        <label for="brush-size">Brush Size</label>
                        <input type="range" id="brush-size" min="1" max="50" value="10">
                        <div class="slider-value" id="brush-size-value">10px</div>
                    </div>
                    
                    <div class="slider-container">
                        <label for="brush-opacity">Opacity</label>
                        <input type="range" id="brush-opacity" min="1" max="100" value="100">
                        <div class="slider-value" id="brush-opacity-value">100%</div>
                    </div>
                </div>
                
                <div class="action-buttons">
                    <button class="btn-action" id="undo-btn">
                        <i class="fas fa-undo"></i> Undo
                    </button>
                    <button class="btn-action" id="redo-btn">
                        <i class="fas fa-redo"></i> Redo
                    </button>
                    <button class="btn-action" id="clear-btn">
                        <i class="fas fa-trash"></i> Clear
                    </button>
                </div>
                
                <div class="auto-save-toggle">
                    <span>Auto-Save</span>
                    <label class="toggle-switch">
                        <input type="checkbox" id="auto-save-toggle">
                        <span class="toggle-slider"></span>
                    </label>
                </div>
                
                <button class="btn-save" id="save-btn">
                    <i class="fas fa-download"></i> Save Artwork
                </button>
            </div>
        </div>
    </div>
    
    <div id="feedback-msg" class="feedback-msg"></div>
    
    <div id="restore-dialog" class="restore-dialog" style="display: none;">
        <div class="restore-dialog-content">
            <h2>Restore Previous Work?</h2>
            <p>We found your previous unsaved artwork. Would you like to continue where you left off?</p>
            <div class="restore-dialog-buttons">
                <button class="btn-new" id="btn-new-canvas">New Canvas</button>
                <button class="btn-restore" id="btn-restore-canvas">Restore</button>
            </div>
        </div>
    </div>
    
    <div id="color-picker-modal" class="color-picker-modal">
        <div class="color-picker-content">
            <h3>Add Custom Color</h3>
            <input type="text" id="custom-color-picker" class="form-control">
            <div class="color-picker-buttons">
                <button class="btn-cancel" id="cancel-color-picker">Cancel</button>
                <button class="btn-add-color" id="confirm-add-color">Add Color</button>
            </div>
        </div>
    </div>
    
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/spectrum-colorpicker2/dist/spectrum.min.js"></script>
    <script id="app-script">
        $(document).ready(function() {
            // Canvas setup
            const canvas = document.getElementById('canvas');
            const ctx = canvas.getContext('2d');
            const canvasLoading = document.getElementById('canvas-loading');
            
            // Canvas state for undo/redo
            const maxStates = 20; // Maximum number of states to store
            let canvasStates = [];
            let currentStateIndex = -1;
            
            // Tool variables
            let currentTool = 'brush';
            let currentColor = '#000000';
            let brushSize = 10;
            let brushOpacity = 1.0;
            let isDrawing = false;
            let lastX = 0;
            let lastY = 0;
            
            // Auto-save settings
            let autoSaveEnabled = false;
            let autoSaveInterval = null;
            const autoSaveDelay = 5000; // 5 seconds
            
            // Initialize canvas size
            function resizeCanvas() {
                const wrapper = document.querySelector('.canvas-wrapper');
                const wrapperWidth = wrapper.clientWidth;
                const wrapperHeight = wrapper.clientHeight;
                
                // Calculate canvas size while maintaining aspect ratio
                const maxWidth = Math.min(wrapperWidth - 40, 1200);
                const maxHeight = Math.min(wrapperHeight - 40, 800);
                
                // Set canvas dimensions
                canvas.width = maxWidth;
                canvas.height = maxHeight;
                
                // Redraw canvas content if there is any
                if (canvasStates.length > 0 && currentStateIndex >= 0) {
                    ctx.drawImage(canvasStates[currentStateIndex], 0, 0);
                } else {
                    // Clear canvas with white background
                    ctx.fillStyle = 'white';
                    ctx.fillRect(0, 0, canvas.width, canvas.height);
                    saveCanvasState();
                }
            }
            
            // Save current canvas state for undo/redo
            function saveCanvasState() {
                // If we're not at the end of the states array, remove all states after current
                if (currentStateIndex < canvasStates.length - 1) {
                    canvasStates = canvasStates.slice(0, currentStateIndex + 1);
                }
                
                // Create an image from the canvas
                const canvasImage = new Image();
                canvasImage.src = canvas.toDataURL();
                
                // Add the state to our states array
                canvasStates.push(canvasImage);
                currentStateIndex = canvasStates.length - 1;
                
                // If we have too many states, remove the oldest one
                if (canvasStates.length > maxStates) {
                    canvasStates.shift();
                    currentStateIndex--;
                }
                
                // Update undo/redo button states
                updateUndoRedoButtons();
            }
            
            // Apply a canvas state (for undo/redo)
            function applyCanvasState(stateIndex) {
                if (stateIndex >= 0 && stateIndex < canvasStates.length) {
                    ctx.clearRect(0, 0, canvas.width, canvas.height);
                    ctx.drawImage(canvasStates[stateIndex], 0, 0);
                    currentStateIndex = stateIndex;
                    updateUndoRedoButtons();
                }
            }
            
            // Update undo/redo buttons state
            function updateUndoRedoButtons() {
                const undoBtn = document.getElementById('undo-btn');
                const redoBtn = document.getElementById('redo-btn');
                
                undoBtn.disabled = currentStateIndex <= 0;
                redoBtn.disabled = currentStateIndex >= canvasStates.length - 1;
                
                // Visual feedback
                undoBtn.style.opacity = undoBtn.disabled ? '0.5' : '1';
                redoBtn.style.opacity = redoBtn.disabled ? '0.5' : '1';
            }
            
            // Drawing functions
            function startDrawing(e) {
                isDrawing = true;
                
                // Get the canvas position relative to the page
                const canvasRect = canvas.getBoundingClientRect();
                
                // Calculate coordinates based on event type
                const clientX = e.type.includes('touch') ? e.touches[0].clientX : e.clientX;
                const clientY = e.type.includes('touch') ? e.touches[0].clientY : e.clientY;
                
                // Set last coordinates
                lastX = clientX - canvasRect.left;
                lastY = clientY - canvasRect.top;
                
                // If color picker tool is active, pick the color instead of drawing
                if (currentTool === 'eyedropper') {
                    const pixelData = ctx.getImageData(lastX, lastY, 1, 1).data;
                    const pickedColor = `#${pixelData[0].toString(16).padStart(2, '0')}${pixelData[1].toString(16).padStart(2, '0')}${pixelData[2].toString(16).padStart(2, '0')}`;
                    setCurrentColor(pickedColor);
                    showFeedback(`Color picked: ${pickedColor}`);
                    return;
                }
                
                // If fill tool is active, fill the area
                if (currentTool === 'fill') {
                    // For now, just fill the entire canvas as a prototype
                    ctx.globalAlpha = brushOpacity;
                    ctx.fillStyle = currentColor;
                    ctx.fillRect(0, 0, canvas.width, canvas.height);
                    ctx.globalAlpha = 1;
                    
                    saveCanvasState();
                    return;
                }
                
                // For other tools, prepare for drawing
                ctx.beginPath();
                
                if (currentTool === 'eraser') {
                    ctx.globalCompositeOperation = 'destination-out';
                    ctx.strokeStyle = 'rgba(255,255,255,1)';
                } else {
                    ctx.globalCompositeOperation = 'source-over';
                    ctx.strokeStyle = currentColor;
                }
                
                ctx.lineWidth = brushSize;
                ctx.lineJoin = 'round';
                ctx.lineCap = 'round';
                ctx.globalAlpha = brushOpacity;
                
                ctx.moveTo(lastX, lastY);
                ctx.lineTo(lastX, lastY);
                ctx.stroke();
            }
            
            function draw(e) {
                if (!isDrawing) return;
                
                // If eyedropper or fill tool is active, don't draw
                if (currentTool === 'eyedropper' || currentTool === 'fill') return;
                
                // Prevent scrolling on touch devices
                e.preventDefault();
                
                // Get the canvas position relative to the page
                const canvasRect = canvas.getBoundingClientRect();
                
                // Calculate coordinates based on event type
                const clientX = e.type.includes('touch') ? e.touches[0].clientX : e.clientX;
                const clientY = e.type.includes('touch') ? e.touches[0].clientY : e.clientY;
                
                // Calculate current position
                const currentX = clientX - canvasRect.left;
                const currentY = clientY - canvasRect.top;
                
                // Draw a line
                ctx.beginPath();
                ctx.moveTo(lastX, lastY);
                
                // Smooth the line based on the tool
                if (currentTool === 'pencil') {
                    // Pencil draws straight line segments
                    ctx.lineTo(currentX, currentY);
                } else {
                    // Brush uses quadratic curves for smoother lines
                    const controlX = (lastX + currentX) / 2;
                    const controlY = (lastY + currentY) / 2;
                    ctx.quadraticCurveTo(lastX, lastY, controlX, controlY);
                }
                
                ctx.stroke();
                
                // Update last position
                lastX = currentX;
                lastY = currentY;
            }
            
            function stopDrawing() {
                if (isDrawing) {
                    isDrawing = false;
                    ctx.globalAlpha = 1;
                    
                    // Save the canvas state for undo/redo
                    if (currentTool !== 'eyedropper') {
                        saveCanvasState();
                        
                        // Auto-save if enabled
                        if (autoSaveEnabled) {
                            saveToLocalStorage();
                        }
                    }
                }
            }
            
            // Auto-save to localStorage
            function saveToLocalStorage() {
                try {
                    localStorage.setItem('canvasData', canvas.toDataURL());
                    showFeedback('Auto-saved!');
                } catch (e) {
                    console.error('Error saving to localStorage', e);
                    showFeedback('Auto-save failed!', true);
                }
            }
            
            // Load from localStorage
            function checkForSavedCanvas() {
                try {
                    const savedCanvas = localStorage.getItem('canvasData');
                    if (savedCanvas) {
                        document.getElementById('restore-dialog').style.display = 'flex';
                    } else {
                        initializeNewCanvas();
                    }
                } catch (e) {
                    console.error('Error checking localStorage', e);
                    initializeNewCanvas();
                }
            }
            
            // Restore canvas from localStorage
            function restoreCanvas() {
                try {
                    const savedCanvas = localStorage.getItem('canvasData');
                    if (savedCanvas) {
                        const img = new Image();
                        img.onload = function() {
                            ctx.clearRect(0, 0, canvas.width, canvas.height);
                            ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
                            saveCanvasState();
                            hideCanvasLoading();
                        };
                        img.src = savedCanvas;
                    } else {
                        initializeNewCanvas();
                    }
                } catch (e) {
                    console.error('Error restoring canvas', e);
                    initializeNewCanvas();
                }
            }
            
            // Initialize a new blank canvas
            function initializeNewCanvas() {
                ctx.fillStyle = 'white';
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                saveCanvasState();
                hideCanvasLoading();
            }
            
            // Set active tool
            function setActiveTool(tool) {
                currentTool = tool;
                
                // Update UI
                document.querySelectorAll('.tool-btn').forEach(btn => {
                    btn.classList.remove('active');
                });
                
                document.getElementById(`${tool}-tool`).classList.add('active');
                
                // Change cursor based on tool
                if (tool === 'eyedropper') {
                    canvas.style.cursor = 'url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsSAAALEgHS3X78AAAA+0lEQVRIie2UMU7DQBBF3xQUKCJFiJIDUCNxAQrOQENLQ0dLm4aWK1AkgtJwCpwGiQNESpHCFsnGjuzx7Cyb0PBLo9nZ+W//rBfWw+YABEAHuAZ+gDnw5NzTBvAAvAPrQnwBl1GZHnDnGC/jCzjJnj8tYFmJ9lmNAvGYG4dxGF+AGyueAq+G+BO4B1KnAdAGnoz8FLgFhn8ZO+IMGBm5EfDsKQDrDnJzlZsCu9kF4F94WpsfmRu4FUKTvATQspwu4NgZd0Nd+/KiYXx9aQVsbfAB1+xDOWrCXGEAHPy2QNxoQa5EZa6ATyM/A7pWvAV0Y1BDvAMcAifAUUXuF/PsITeK0cYwAAAAAElFTkSuQmCC) 12 12, auto';
                } else if (tool === 'fill') {
                    canvas.style.cursor = 'url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsSAAALEgHS3X78AAABA0lEQVRIie2UMU7DQBBF3xQp0lBEiHAACiQuQME5aGhp6GhpuQEtV6BIBN0egHNQ5ACREiRKVGQjr+NdZsc7MU3+016tZ/6f9a5XfA1PgQh4At6AjXPOYOQFsAbWmXkH4hR0DdwDr8ASCIDTE8KS4ANYZGsf8jNdIBGvgIchxOVRUCcuJ3Uf+bkqKMRLINS46PQzMM/XkrW/WlxqS44KHXGOwP81RU28C/tqKq6Vx+ZHFLiwCoC5Md9xzR6Vrybin0CFKWwKeDDmO6Lm2+VpK9oCi4bxzaMtEDQlcjQKcYUMmBnzM2Bk5QPgxgVZzKG4pGgJPNe83xGPC2fVnIq+AU2PKZ9j2Xy2AAAAAElFTkSuQmCC) 12 12, auto';
                } else if (tool === 'eraser') {
                    canvas.style.cursor = 'url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsSAAALEgHS3X78AAAA2ElEQVRIie2UMQrCQBBFXyxs7AQLwdJT2Hkry5zCxt7OE3gAey/gAbQQC2thGpvVdTKTbGIg7odhJpP5f3dnA/m6/kBegeXEOANq4NwlUACHTMYj0nMYSQvoQWPkjzwnMwYkVqUgZV6Arh3AZmDeBnJcxxXQ2qQlsA4MLBvGRSLGy2sTmqxKC8g9vYJ8BfkK/rtAvK8XEbO6AU5m7w5sv7UkRhHJuw0UNw1l3gCX0KVKxNR+nJ+IIXOziZn3fVEDBdFwmIcUJuYS3h8k5hJlZNAE1aRJZV4DdwBmKqQXG6FzAAAAAElFTkSuQmCC) 12 12, auto';
                } else if (tool === 'pencil') {
                    canvas.style.cursor = 'url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsSAAALEgHS3X78AAAA5ElEQVRIie3UsUrDUBTG8V9sBRfBQXBx7lO4+SC+Qp9Ddy/g5uYLOLj4Bl2cXRVcHBwEB4UiKA6xmuPNbaIpueSm/OFwc3O+8587nHBerUy3oQ0c4wYPGI4LmGGgwhle8Y5bXKEXm7zECp7wVcg77rATm1xhiElAvuMCuyjnZxMQbAckQqYkdLCOn0WSZzGqZIQu1hJIVo1xij7yUGKZRu9fAjrVn+EvxjCFDCNa4A2H4drsFW1Ej8JXlKxhDwcJJNVTdIgzPCYWuI8O6Gw4/Rq3+MAl9lPI0lnMQlYjkh3iBn/1DYdIQxn77QD8AAAAAElFTkSuQmCC) 12 12, auto';
                } else {
                    canvas.style.cursor = 'url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsSAAALEgHS3X78AAAA4ElEQVRIie3UvUpDQRDG8d9pBC0sbGwstZI0FtY+gg+hjY2FYG+jD2DvC/gAYmfjA9hYaSMWgoWFYGFhkSJ6xON6srvJXiH3wMDB7M58/5mdg+f1cwH7mOEOz5gW6j0sYRmXeKvMZzgsND7CGG+FzHCLNmaxQSrLg3zHQ8TrqfE0NPnVOI+pYXFKPf9aMz7HdSFjCfbqDE7wWchR8NBiZQEP6BWyCh5J1+RJg0nG2ApfRnmN4Bxvmc8NnI6L/hRwgh4WMuZu8DLY4DL8c4JzHGCnxmQdq9jERmD8jlvcY4DxJ2EPO3NR7UxFAAAAAElFTkSuQmCC) 12 12, auto';
                }
                
                showFeedback(`${tool.charAt(0).toUpperCase() + tool.slice(1)} tool selected`);
            }
            
            // Set current color
            function setCurrentColor(color) {
                currentColor = color;
                
                // Update UI
                document.querySelectorAll('.color-swatch').forEach(swatch => {
                    swatch.classList.remove('active');
                    if (swatch.getAttribute('data-color') === color) {
                        swatch.classList.add('active');
                    }
                });
            }
            
            // Show feedback message
            function showFeedback(message, isError = false) {
                const feedbackElement = document.getElementById('feedback-msg');
                feedbackElement.textContent = message;
                feedbackElement.style.backgroundColor = isError ? 'rgba(220, 53, 69, 0.8)' : 'rgba(0, 0, 0, 0.7)';
                feedbackElement.classList.add('show');
                
                setTimeout(() => {
                    feedbackElement.classList.remove('show');
                }, 2000);
            }
            
            // Show canvas loading
            function showCanvasLoading() {
                canvasLoading.style.display = 'flex';
            }
            
            // Hide canvas loading
            function hideCanvasLoading() {
                canvasLoading.style.display = 'none';
            }
            
            // Download canvas as image
            function downloadCanvas() {
                showFeedback('Preparing download...');
                
                try {
                    const link = document.createElement('a');
                    link.download = `canvas-creation-${new Date().toISOString().slice(0, 10)}.png`;
                    link.href = canvas.toDataURL('image/png');
                    link.click();
                    showFeedback('Image downloaded successfully!');
                } catch (e) {
                    console.error('Error downloading canvas', e);
                    showFeedback('Download failed!', true);
                }
            }
            
            // Event listeners
            function setupEventListeners() {
                // Canvas drawing events
                canvas.addEventListener('mousedown', startDrawing);
                canvas.addEventListener('mousemove', draw);
                canvas.addEventListener('mouseup', stopDrawing);
                canvas.addEventListener('mouseout', stopDrawing);
                
                // Touch support
                canvas.addEventListener('touchstart', startDrawing);
                canvas.addEventListener('touchmove', draw);
                canvas.addEventListener('touchend', stopDrawing);
                canvas.addEventListener('touchcancel', stopDrawing);
                
                // Tool selection
                document.getElementById('brush-tool').addEventListener('click', () => setActiveTool('brush'));
                document.getElementById('pencil-tool').addEventListener('click', () => setActiveTool('pencil'));
                document.getElementById('eraser-tool').addEventListener('click', () => setActiveTool('eraser'));
                document.getElementById('fill-tool').addEventListener('click', () => setActiveTool('fill'));
                document.getElementById('eyedropper-tool').addEventListener('click', () => setActiveTool('eyedropper'));
                
                // Color swatches
                document.querySelectorAll('.color-swatch').forEach(swatch => {
                    swatch.addEventListener('click', () => {
                        const color = swatch.getAttribute('data-color');
                        setCurrentColor(color);
                    });
                });
                
                // Add color button
                document.getElementById('add-color-btn').addEventListener('click', () => {
                    document.getElementById('color-picker-modal').style.display = 'flex';
                });
                
                // Color picker modal
                document.getElementById('cancel-color-picker').addEventListener('click', () => {
                    document.getElementById('color-picker-modal').style.display = 'none';
                });
                
                document.getElementById('confirm-add-color').addEventListener('click', addCustomColor);
                
                // Brush settings
                document.getElementById('brush-size').addEventListener('input', function() {
                    brushSize = parseInt(this.value);
                    document.getElementById('brush-size-value').textContent = `${brushSize}px`;
                });
                
                document.getElementById('brush-opacity').addEventListener('input', function() {
                    brushOpacity = parseInt(this.value) / 100;
                    document.getElementById('brush-opacity-value').textContent = `${this.value}%`;
                });
                
                // Action buttons
                document.getElementById('undo-btn').addEventListener('click', () => {
                    if (currentStateIndex > 0) {
                        applyCanvasState(currentStateIndex - 1);
                        showFeedback('Undo successful');
                    }
                });
                
                document.getElementById('redo-btn').addEventListener('click', () => {
                    if (currentStateIndex < canvasStates.length - 1) {
                        applyCanvasState(currentStateIndex + 1);
                        showFeedback('Redo successful');
                    }
                });
                
                document.getElementById('clear-btn').addEventListener('click', () => {
                    if (confirm('Are you sure you want to clear the canvas?')) {
                        ctx.fillStyle = 'white';
                        ctx.fillRect(0, 0, canvas.width, canvas.height);
                        saveCanvasState();
                        showFeedback('Canvas cleared');
                    }
                });
                
                // Save button
                document.getElementById('save-btn').addEventListener('click', downloadCanvas);
                
                // Auto-save toggle
                document.getElementById('auto-save-toggle').addEventListener('change', function() {
                    autoSaveEnabled = this.checked;
                    
                    if (autoSaveEnabled) {
                        autoSaveInterval = setInterval(saveToLocalStorage, autoSaveDelay);
                        showFeedback('Auto-save enabled');
                    } else {
                        clearInterval(autoSaveInterval);
                        showFeedback('Auto-save disabled');
                    }
                });
                
                // Restore dialog
                document.getElementById('btn-new-canvas').addEventListener('click', () => {
                    document.getElementById('restore-dialog').style.display = 'none';
                    localStorage.removeItem('canvasData');
                    initializeNewCanvas();
                });
                
                document.getElementById('btn-restore-canvas').addEventListener('click', () => {
                    document.getElementById('restore-dialog').style.display = 'none';
                    restoreCanvas();
                });
                
                // Window resize event
                window.addEventListener('resize', resizeCanvas);
            }
            
            // Initialize spectrum color picker
            function initializeColorPicker() {
                $("#custom-color-picker").spectrum({
                    color: currentColor,
                    showInput: true,
                    showPalette: true,
                    preferredFormat: "hex",
                    showInitial: true,
                    palette: [
                        ["#000", "#444", "#666", "#999", "#ccc", "#eee", "#f3f3f3", "#fff"],
                        ["#f00", "#f90", "#ff0", "#0f0", "#0ff", "#00f", "#90f", "#f0f"],
                        ["#f4cccc", "#fce5cd", "#fff2cc", "#d9ead3", "#d0e0e3", "#cfe2f3", "#d9d2e9", "#ead1dc"],
                        ["#ea9999", "#f9cb9c", "#ffe599", "#b6d7a8", "#a2c4c9", "#9fc5e8", "#b4a7d6", "#d5a6bd"],
                        ["#e06666", "#f6b26b", "#ffd966", "#93c47d", "#76a5af", "#6fa8dc", "#8e7cc3", "#c27ba0"],
                        ["#c00", "#e69138", "#f1c232", "#6aa84f", "#45818e", "#3d85c6", "#674ea7", "#a64d79"],
                        ["#900", "#b45f06", "#bf9000", "#38761d", "#134f5c", "#0b5394", "#351c75", "#741b47"],
                        ["#600", "#783f04", "#7f6000", "#274e13", "#0c343d", "#073763", "#20124d", "#4c1130"]
                    ]
                });
            }
            
            // Add a custom color to the palette
            function addCustomColor() {
                const colorPicker = $("#custom-color-picker");
                const newColor = colorPicker.spectrum("get").toHexString();
                
                // Create new color swatch
                const colorSwatch = document.createElement('div');
                colorSwatch.classList.add('color-swatch');
                colorSwatch.style.backgroundColor = newColor;
                colorSwatch.setAttribute('data-color', newColor);
                
                // Add event listener
                colorSwatch.addEventListener('click', () => {
                    setCurrentColor(newColor);
                });
                
                // Add to palette before the "add" button
                const addColorBtn = document.getElementById('add-color-btn');
                addColorBtn.parentNode.insertBefore(colorSwatch, addColorBtn);
                
                // Close the modal and set the new color as current
                document.getElementById('color-picker-modal').style.display = 'none';
                setCurrentColor(newColor);
                
                showFeedback(`New color ${newColor} added`);
            }
            
            // Initialize the app
            function initializeApp() {
                showCanvasLoading();
                
                // Initialize the canvas
                resizeCanvas();
                
                // Setup event listeners
                setupEventListeners();
                
                // Initialize color picker
                initializeColorPicker();
                
                // Check for saved canvas
                checkForSavedCanvas();
                
                // Initialize brush settings display
                document.getElementById('brush-size-value').textContent = `${brushSize}px`;
                document.getElementById('brush-opacity-value').textContent = `${brushOpacity * 100}%`;
                
                // Set initial tool
                setActiveTool('brush');
                
                // Set initial color
                setCurrentColor('#000000');
            }
            
            // Start the app
            initializeApp();
        });
    </script>
    
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
</body>
</html>
