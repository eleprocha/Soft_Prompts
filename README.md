import streamlit as st

# Set page configuration
st.set_page_config(
    page_title="Soft  Prompt Fine-Tuning",
    page_icon="🤖",
    layout="wide",
    initial_sidebar_state="collapsed"
)

# HTML content for the presentation
html_content = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Transformer Models Presentation</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .presentation-container {
            width: 90vw;
            height: 90vh;
            background: white;
            border-radius: 10px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            position: relative;
            overflow: hidden;
        }

        .slide {
            width: 100%;
            height: 100%;
            position: absolute;
            display: none;
            padding: 60px 80px;
            background: white;
        }

        .slide.active {
            display: flex;
            flex-direction: column;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateX(20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .slide-header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: #FFD700;
            padding: 30px 40px;
            margin: -60px -80px 40px -80px;
            border-bottom: 5px solid #FFD700;
        }

        .slide-header h1 {
            font-size: 48px;
            font-weight: 700;
            margin-bottom: 10px;
        }

        .slide-header h2 {
            font-size: 36px;
            font-weight: 600;
            margin-bottom: 5px;
        }

        .slide-header p {
            font-size: 20px;
            color: #FFF9C4;
            margin-top: 10px;
        }

        .content {
            flex: 1;
            overflow-y: auto;
            color: #1e3c72;
        }

        h3 {
            color: #1e3c72;
            font-size: 32px;
            margin: 25px 0 15px 0;
            border-left: 6px solid #FFD700;
            padding-left: 20px;
        }

        .model-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 25px;
            margin: 30px 0;
        }

        .model-card {
            background: linear-gradient(135deg, #2a5298 0%, #1e3c72 100%);
            color: white;
            padding: 25px;
            border-radius: 10px;
            border: 3px solid #FFD700;
            transition: transform 0.3s ease;
        }

        .model-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(255, 215, 0, 0.3);
        }

        .model-card h4 {
            color: #FFD700;
            font-size: 24px;
            margin-bottom: 15px;
        }

        .model-card p {
            font-size: 16px;
            line-height: 1.6;
        }

        ul {
            margin: 20px 0 20px 40px;
            line-height: 2;
        }

        li {
            font-size: 20px;
            margin: 10px 0;
            color: #2a5298;
        }

        li strong {
            color: #1e3c72;
        }

        .lab-section {
            background: #FFF9C4;
            border-left: 6px solid #1e3c72;
            padding: 25px;
            margin: 20px 0;
            border-radius: 5px;
        }

        .lab-section h4 {
            color: #1e3c72;
            font-size: 24px;
            margin-bottom: 15px;
        }

        .lab-section p {
            color: #2a5298;
            font-size: 18px;
            line-height: 1.7;
        }

        .controls {
            position: absolute;
            bottom: 30px;
            right: 30px;
            display: flex;
            gap: 15px;
            z-index: 100;
        }

        button {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: #FFD700;
            border: 2px solid #FFD700;
            padding: 12px 30px;
            font-size: 18px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        button:hover {
            background: #FFD700;
            color: #1e3c72;
            transform: scale(1.05);
        }

        button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .slide-number {
            position: absolute;
            bottom: 30px;
            left: 30px;
            background: #1e3c72;
            color: #FFD700;
            padding: 10px 20px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 16px;
        }

        .highlight-box {
            background: linear-gradient(135deg, #2a5298 0%, #1e3c72 100%);
            color: white;
            padding: 20px 30px;
            border-radius: 10px;
            margin: 20px 0;
            border-left: 6px solid #FFD700;
        }

        .two-column {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin: 20px 0;
        }
    </style>
</head>
<body>
    <div class="presentation-container">
        <!-- Slide 1: Title -->
        <div class="slide active">
            <div class="slide-header">
                <h1>🤖 Soft Prompts</h1>
                <p>Soft prompting is a technique that enhances the behavior of large language models (LLMs) by optimizing continuous prompt embeddings rather than manually writing textual prompts. Instead of using only human-written instructions (e.g., “Translate this to French”), soft prompts learn short vectors that guide the model toward a desired task, domain, or style — without updating the model’s internal weights.</p>
            </div>
            <div class="content" style="display: flex; justify-content: center; align-items: center;">
                <div style="text-align: center;">
                    <h2 style="color: #1e3c72; font-size: 42px; margin-bottom: 30px;">What Soft Promts Are</h2>
                    <div style="display: flex; justify-content: space-around; align-items: center; gap: 40px;">
                        <div style="text-align: center;">
                            <div style="font-size: 80px; color: #FFD700;">📝</div>
                            <h3 style="border: none; padding: 0; margin-top: 15px;">Trainable embedding vectors</h3>
                            <p style="color: #2a5298; font-size: 20px;">A soft prompt is a small set of trainable embedding vectors prepended to the input text.</p>
                        </div>
                        <div style="text-align: center;">
                            <div style="font-size: 80px; color: #FFD700;">🔍</div>
                            <h3 style="border: none; padding: 0; margin-top: 15px;">Task Hint or Instruction</h3>
                            <p style="color: #2a5298; font-size: 20px;">These vectors act like a learned “task hint” or “instruction” that the model reads before the real user input.</p>
                        </div>
                        <div style="text-align: center;">
                            <div style="font-size: 80px; color: #FFD700;">🌐</div>
                            <h3 style="border: none; padding: 0; margin-top: 15px;">Encode richer signals</h3>
                            <p style="color: #2a5298; font-size: 20px;">Because the vectors live in embedding space, they can encode richer signals than plain text.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 2: Overview -->
        <div class="slide">
            <div class="slide-header">
                <h2>📋 Why Soft Prompts Matter</h2>
            </div>
            <div class="content">
                <div class="model-grid">
                    <div class="model-card">
                        <h4>🎯 Lightweight & cheap to train</h4>
                        <p>Only a handful of vectors are optimized</p>
                    </div>
                    <div class="model-card">
                        <h4>🎯 Interpretation-friendly</h4>
                        <p>They control behavior without modifying the core model</p>
                    </div>
                    <div class="model-card">
                        <h4>🎯 No full fine-tuning required</h4>
                        <p>Avoids updating billions of model parameters</p>
                    </div>
                </div>

                <h3>How Soft Prompts Work</h3>
                <ul>
                    <li><strong>Soft prompts are learned through gradient descent:</li>
                    <ul>
                        <li>The model parameters are frozen.</li>
                        <li>Only the added prompt embeddings are trainable.</li>
                        <li>During training, gradients flow into the soft prompt but not the model itself.</li>
                        <li>You can think of this as teaching the model a new “prefix” that tells it how to behave.</li>
                    </ul>
                </ul>
            </div>
        </div>

        <!-- Slide 3: Decoder Models -->
        <div class="slide">
            <div class="slide-header">
                <h2>📝 Types of Soft Prompting</h2>
            </div>
            <div class="content">
                <div class="highlight-box">
                    <h4 style="color: #FFD700; font-size: 24px; margin-bottom: 10px;">💡 A. Prompt-Tuning</h4>
                </div>

                <div class="two-column">
                    <div>
                        <h4 style="color: #1e3c72; font-size: 22px; margin-bottom: 15px;">🎭 The classic Method</h4>
                        <ul style="margin-left: 20px;">
                            <li>Inserts soft prompt embeddings before the input.</li>
                            <li>Works well for classification and simple tasks.</li>
                        </ul>
                    </div>
                    <div>
                        <h4 style="color: #1e3c72; font-size: 22px; margin-bottom: 15px;">⚙️ Implementation</h4>
                        <ul style="margin-left: 20px;">
                            <img src="p_tunning.png" style="width:500px; height:300px;">
                        </ul>
                    </div>
                </div>
            </div>
        </div>

         <div class="slide">
            <div class="slide-header">
                <h2>📝 Types of Soft Prompting</h2>
            </div>
            <div class="content">
                <div class="highlight-box">
                    <h4 style="color: #FFD700; font-size: 24px; margin-bottom: 10px;">💡 B. Prefix-Tunning</h4>
                </div>

                <div class="two-column">
                    <div>
                        <ul style="margin-left: 20px;">
                            <li>Tuning closely resembles prompt tuning, as both involve adding task-specific vectors to the input</li>
                            <li>These vectors are adjusted and updated while the rest of the pre-trained model's parameters remain unchanged</li>
                            <li>The key dinstinction is the prefix tuning integrates these parameters across all model layers, unlike prompt tunning which only modifies the input embedings.</li>
                            <li>Prefix parameters are optimised using a seperate feed-forward network (FFN) to avoid instability and performance issues.</li>
                            <li>Once the soft prompts are updated, the FFN is removed.</li>
                        </ul>
                    </div>
                    <div>
                        <h4 style="color: #1e3c72; font-size: 22px; margin-bottom: 15px;">⚙️ Implementation</h4>
                        <ul style="margin-left: 20px;">
                            <img src="prefix_tunning.png" style="width:500px; height:300px;">
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        

        <!-- Slide 6: Lab 1 -->
        <div class="slide">
            <div class="slide-header">
                <h2>Best Practices for using soft prompts</h2>
            </div>
            <div class="content">
                <div class="lab-section">
                    <h4>🎯 Leverage the full potential of soft prompts and their effectiveness</h4>
                </div>

                <h3>Key Concepts</h3>
                <ul>
                    <li><strong>Robust Pre-trained model</strong> This acts as a base to ensure that the soft prompts can effectively leverage the existing knowledge</li>
                    <li>The diverse and representative data ensures the data sets are fine-tuned for the tasks for learning and generalizing the soft prompts</li>
                    <li><strong>Evaluating the model's performance:</strong> Adjusting the soft prompts enhances the model's performance</li>
                    <li><strong>Monitor Data Overfitting:</strong> Cross Validation monitors the data overfitting to supervise the model's performance on the unseen data</li>
                </ul>


            </div>
        </div>

        <!-- Slide 7: Lab 2 -->
        <div class="slide">
            <div class="slide-header">
                <h2>🔬 Benefits of Soft Prompts</h2>
            </div>
            <div class="content">
                <div class="two-column" style="margin-top: 25px;">
                    <div class="highlight-box">
                        <h4 style="color: #FFD700; margin-bottom: 20px;">📚 Efficiency</h4>
                        <p>• Increase task adaption</p>
                        <p>• Fewer resources than full model fine-tuning</p>
                        <p>• Optimising only a small subset of parameters</p>
                    </div>
                    <div class="highlight-box">
                        <h4 style="color: #FFD700; margin-bottom: 20px;">🚀 Flexibility</h4>
                        <p>• Help in dynamic enironment where requirements change frequently</p>
                        <p>• Fine-tune models for text classification</p>
                    </div>
                    <div class="highlight-box">
                        <h4 style="color: #FFD700; margin-bottom: 20px;">🚀 Scalability</h4>
                        <p>• Easy to scale for different models and datasets</p>
                        <p>• Robust solution for diverse NLP Tasks</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Navigation -->
        <div class="slide-number">
            <span id="currentSlide">1</span> / <span id="totalSlides">9</span>
        </div>

        <div class="controls">
            <button id="prevBtn" onclick="changeSlide(-1)">← Previous</button>
            <button id="nextBtn" onclick="changeSlide(1)">Next →</button>
        </div>
    </div>

    <script>
        let currentSlide = 0;
        const slides = document.querySelectorAll('.slide');
        const totalSlides = slides.length;
        
        document.getElementById('totalSlides').textContent = totalSlides;

        function showSlide(n) {
            slides[currentSlide].classList.remove('active');
            currentSlide = (n + totalSlides) % totalSlides;
            slides[currentSlide].classList.add('active');
            
            document.getElementById('currentSlide').textContent = currentSlide + 1;
            
            document.getElementById('prevBtn').disabled = currentSlide === 0;
            document.getElementById('nextBtn').disabled = currentSlide === totalSlides - 1;
        }

        function changeSlide(direction) {
            showSlide(currentSlide + direction);
        }

        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft') changeSlide(-1);
            if (e.key === 'ArrowRight') changeSlide(1);
        });

        showSlide(0);
    </script>
</body>
</html>
"""

# Display the HTML presentation
st.components.v1.html(html_content, height=800, scrolling=False)

# Add footer with instructions
st.markdown("---")
