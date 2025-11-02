# sczsanmcfasnjm
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اختبار خواص المادة - 50 سؤالًا</title>
    <style>
        :root {
            --primary-color: #3498db;
            --secondary-color: #2c3e50;
            --correct-color: #2ecc71;
            --incorrect-color: #e74c3c;
            --light-color: #ecf0f1;
            --dark-color: #34495e;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: var(--dark-color);
            line-height: 1.6;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 1.5rem;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            font-size: 2rem;
            margin-bottom: 0.5rem;
        }
        
        .container {
            max-width: 800px;
            margin: 2rem auto;
            padding: 0 1rem;
        }
        
        .intro {
            background-color: white;
            padding: 1.5rem;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin-bottom: 2rem;
            text-align: center;
        }
        
        .question-container {
            background-color: white;
            padding: 1.5rem;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin-bottom: 1.5rem;
        }
        
        .question-number {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--primary-color);
            margin-bottom: 0.5rem;
        }
        
        .question-text {
            font-size: 1.1rem;
            margin-bottom: 1rem;
        }
        
        .options {
            display: flex;
            flex-direction: column;
            gap: 0.8rem;
        }
        
        .option {
            display: flex;
            align-items: center;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .option:hover {
            background-color: #f9f9f9;
        }
        
        .option.selected {
            background-color: #e3f2fd;
            border-color: var(--primary-color);
        }
        
        .option.correct {
            background-color: var(--correct-color);
            color: white;
        }
        
        .option.incorrect {
            background-color: var(--incorrect-color);
            color: white;
        }
        
        .option input {
            margin-left: 10px;
        }
        
        .option label {
            flex: 1;
            cursor: pointer;
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 1.5rem;
        }
        
        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 0.7rem 1.5rem;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: var(--secondary-color);
        }
        
        button:disabled {
            background-color: #bdc3c7;
            cursor: not-allowed;
        }
        
        .progress-bar {
            height: 8px;
            background-color: #e0e0e0;
            border-radius: 4px;
            margin: 1rem 0;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background-color: var(--primary-color);
            width: 0%;
            transition: width 0.3s;
        }
        
        .results {
            background-color: white;
            padding: 2rem;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            text-align: center;
            display: none;
        }
        
        .score {
            font-size: 2rem;
            font-weight: bold;
            color: var(--primary-color);
            margin: 1rem 0;
        }
        
        .restart-btn {
            margin-top: 1.5rem;
        }
        
        .section-title {
            font-size: 1.3rem;
            color: var(--secondary-color);
            margin: 1.5rem 0 1rem;
            padding-bottom: 0.5rem;
            border-bottom: 2px solid var(--primary-color);
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 0 0.5rem;
            }
            
            .question-container {
                padding: 1rem;
            }
            
            h1 {
                font-size: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>اختبار خواص المادة</h1>
        <p>50 سؤالًا اختيار من متعدد</p>
    </header>
    
    <div class="container">
        <div class="intro">
            <h2>مرحبًا بك في اختبار خواص المادة</h2>
            <p>يتكون هذا الاختبار من 50 سؤالًا حول حالات المادة، الخواص الفيزيائية والكيميائية، والتغيرات المختلفة.</p>
            <p>اختر الإجابة الصحيحة لكل سؤال ثم اضغط على "التالي" للمتابعة.</p>
            <button id="start-btn">ابدأ الاختبار</button>
        </div>
        
        <div id="quiz-container" style="display: none;">
            <div class="progress-bar">
                <div class="progress" id="progress"></div>
            </div>
            
            <div id="question-section"></div>
            
            <div class="navigation">
                <button id="prev-btn" disabled>السابق</button>
                <button id="next-btn">التالي</button>
            </div>
        </div>
        
        <div class="results" id="results">
            <h2>نتيجة الاختبار</h2>
            <div class="score" id="score">0/50</div>
            <p id="result-message"></p>
            <button class="restart-btn" id="restart-btn">إعادة الاختبار</button>
        </div>
    </div>

    <script>
        // أسئلة الاختبار
        const questions = [
            {
                section: "حالات المادة",
                question: "أي مما يلي يُعدّ من حالات المادة الأساسية؟",
                options: ["البلازما", "الصلبة", "الغروبة"],
                correct: 0
            },
            {
                section: "حالات المادة",
                question: "أي خاصية تُميز المادة الصلبة؟",
                options: ["ليس لها حجم ثابت", "لها شكل ثابت", "تنضغط بسهولة"],
                correct: 1
            },
            {
                section: "حالات المادة",
                question: "أي مما يلي يُعدّ من خصائص السوائل؟",
                options: ["شكل ثابت", "حجم ثابت", "يمكن ضغطها بشدة"],
                correct: 1
            },
            {
                section: "حالات المادة",
                question: "الغازات تتميز بأنها؟",
                options: ["لها شكل وحجم ثابت", "ليس لها شكل أو حجم ثابت", "لا تتحرك جسيماتها"],
                correct: 1
            },
            {
                section: "حالات المادة",
                question: "أي مما يلي مثال على بخار؟",
                options: ["بخار الماء", "غاز الأكسجين", "غاز ثاني أكسيد الكربون"],
                correct: 0
            },
            {
                section: "الخواص الفيزيائية والكيميائية",
                question: "أي خاصية يمكن ملاحظتها دون تغيير تركيب المادة؟",
                options: ["فيزيائية", "كيميائية", "نوية"],
                correct: 0
            },
            {
                section: "الخواص الفيزيائية والكيميائية",
                question: "أي من الخواص التالية تُعدّ خاصية فيزيائية؟",
                options: ["الكثافة", "التفاعل مع الأحماض", "الانشعال"],
                correct: 0
            },
            {
                section: "الخواص الفيزيائية والكيميائية",
                question: "أي من الخواص التالية تُعدّ خاصية كيميائية؟",
                options: ["القابلية للانشعال", "الكتلة", "الطول"],
                correct: 0
            },
            {
                section: "الخواص الفيزيائية والكيميائية",
                question: "الكثافة تُعدّ من الخواص؟",
                options: ["الشدة", "الممتدة", "الكيميائية"],
                correct: 0
            },
            {
                section: "الخواص الفيزيائية والكيميائية",
                question: "الطول يُعدّ من الخواص:",
                options: ["نوعية", "كمية", "كيميائية"],
                correct: 1
            },
            {
                section: "التغيرات الفيزيائية والكيميائية",
                question: "عند إذابة الملح في الماء فإن ذلك:",
                options: ["تغير فيزيائي", "تغير كيميائي", "إنتاج مادة جديدة"],
                correct: 0
            },
            {
                section: "التغيرات الفيزيائية والكيميائية",
                question: "احتراق الخشب يُعدّ:",
                options: ["تغير فيزيائي", "تغير كيميائي", "تغير شكلي"],
                correct: 1
            },
            {
                section: "التغيرات الفيزيائية والكيميائية",
                question: "انكسار الزجاج مثال على:",
                options: ["تغير كيميائي", "تغير فيزيائي", "نموي"],
                correct: 1
            },
            {
                section: "التغيرات الفيزيائية والكيميائية",
                question: "صدأ الحديد يمثل:",
                options: ["تغير فيزيائي", "تغير كيميائي", "خاصية فيزيائية"],
                correct: 1
            },
            {
                section: "التغيرات الفيزيائية والكيميائية",
                question: "تبخر الماء مثال على:",
                options: ["تغير كيميائي", "تغير فيزيائي", "لا تغير"],
                correct: 1
            },
            {
                section: "التغيرات الفيزيائية والكيميائية",
                question: "قلي البيض يُعدّ:",
                options: ["تغير فيزيائي", "تغير كيميائي", "انصهار"],
                correct: 1
            },
            {
                section: "التغيرات الفيزيائية والكيميائية",
                question: "تخمر العسل يُعتبر:",
                options: ["تغير فيزيائي", "تغير كيميائي", "تغير شكلي"],
                correct: 1
            },
            {
                section: "تأثير العوامل الخارجية",
                question: "أي عامل يؤثر في حالة المادة؟",
                options: ["درجة الحرارة", "اللون", "الطول"],
                correct: 0
            },
            {
                section: "تأثير العوامل الخارجية",
                question: "عند تسخين الجليد فإنه يتحول إلى:",
                options: ["غاز", "سائل", "صلب آخر"],
                correct: 1
            },
            {
                section: "تأثير العوامل الخارجية",
                question: "عملية تحول المادة من صلب إلى سائل تسمى:",
                options: ["تبخر", "انصهار", "تكثف"],
                correct: 1
            },
            {
                section: "تأثير العوامل الخارجية",
                question: "تحول الغاز إلى سائل يسمى:",
                options: ["تبخر", "انصهار", "تكثف"],
                correct: 2
            },
            {
                section: "تأثير العوامل الخارجية",
                question: "العملية التي تتحول فيها المادة الصلبة مباشرة إلى غاز:",
                options: ["ترشيح", "تسامي", "تبلور"],
                correct: 1
            },
            {
                section: "الخواص الممتدة والشدة",
                question: "أي خاصية تعتمد على كمية المادة؟",
                options: ["الحجم", "الكثافة", "اللون"],
                correct: 0
            },
            {
                section: "الخواص الممتدة والشدة",
                question: "الكتلة يُعتبر خاصية:",
                options: ["ممتدة", "نوعية", "كيميائية"],
                correct: 0
            },
            {
                section: "الخواص الممتدة والشدة",
                question: "اللون يُعتبر خاصية:",
                options: ["كيميائية", "نوعية", "ممتدة"],
                correct: 1
            },
            {
                section: "الخواص الممتدة والشدة",
                question: "الخاصية التي لا تتغير بتغير كمية المادة:",
                options: ["الحجم", "الكثافة", "الكتلة"],
                correct: 1
            },
            {
                section: "أمثلة وتطبيقات",
                question: "الشمع عند درجة حرارة الغرفة يُعتبر مادة:",
                options: ["صلبة", "سائلة", "غازية"],
                correct: 0
            },
            {
                section: "أمثلة وتطبيقات",
                question: "الخشب يطفو على الماء لأن:",
                options: ["كثافته أقل من كثافة الماء", "حجمه كبير", "وزنه صغير"],
                correct: 0
            },
            {
                section: "أمثلة وتطبيقات",
                question: "عند تجمد الماء فإن حجمه:",
                options: ["يزداد", "ينقص", "يبقى ثابتاً"],
                correct: 0
            },
            {
                section: "أمثلة وتطبيقات",
                question: "النحاس موصل جيد للكهرباء، وهذا مثال على خاصية:",
                options: ["كيميائية", "فيزيائية", "نووية"],
                correct: 1
            },
            {
                section: "أمثلة وتطبيقات",
                question: "حشوة الأسنان غالبًا ما تصنف على أنها:",
                options: ["عنصر", "مركب", "محلول صلب"],
                correct: 2
            },
            {
                section: "أمثلة وتطبيقات",
                question: "سبيكة الحديد والنحاس تعتبر:",
                options: ["محلول صلب-صلب", "محلول سائل-صلب", "محلول سائل-سائل"],
                correct: 0
            },
            {
                section: "أمثلة وتطبيقات",
                question: "عند التحليل الكهربائي للماء تكون نسبة الهيدروجين إلى الأكسجين:",
                options: ["1:1", "2:1", "3:1"],
                correct: 1
            },
            {
                section: "أمثلة وتطبيقات",
                question: "تفاعل الصوديوم مع الماء مثال على:",
                options: ["تغير فيزيائي", "تغير كيميائي", "لا تغير"],
                correct: 1
            },
            {
                section: "أمثلة وتطبيقات",
                question: "عند غليان الماء فإنه:",
                options: ["يتغير تركيبه", "يتغير حالته فقط", "يتكون مركب جديد"],
                correct: 1
            },
            {
                section: "من قوانين المادة",
                question: "القانون الذي يفسر ثبات الكتلة في التفاعلات:",
                options: ["قانون النسب الثابتة", "قانون حفظ الكتلة", "قانون النسب المتضاعفة"],
                correct: 1
            },
            {
                section: "من قوانين المادة",
                question: "CO و CO₂ مثال على:",
                options: ["النسب الثابتة", "حفظ الكتلة", "النسب المتضاعفة"],
                correct: 2
            },
            {
                section: "من قوانين المادة",
                question: "التغير الفيزيائي يتميز ب:",
                options: ["عدم تكوين مادة جديدة", "تكوين مادة جديدة", "إنتاج حرارة دائمًا"],
                correct: 0
            },
            {
                section: "من قوانين المادة",
                question: "أي مما يلي دليل على حدوث تغير كيميائي؟",
                options: ["انكسار الشكل", "تغير اللون", "التبخر"],
                correct: 1
            },
            {
                section: "من قوانين المادة",
                question: "تكوين رائحة جديدة أثناء التفاعل دليل على:",
                options: ["تغير فيزيائي", "تغير كيميائي", "لا تغير"],
                correct: 1
            },
            {
                section: "تطبيقات حسابية مبسطة",
                question: "إذا تفاعلت 16.6g من المغنيسيوم مع 10g من الأكسجين تكون كتلة الناتج MgO:",
                options: ["6.6g", "26.6g", "106.6g"],
                correct: 1
            },
            {
                section: "تطبيقات حسابية مبسطة",
                question: "عينة كتلتها 100g من مركب تحتوي على 20g هيدروجين، النسبة المئوية للهيدروجين =",
                options: ["11%", "21%", "31%"],
                correct: 1
            },
            {
                section: "تطبيقات حسابية مبسطة",
                question: "مركب يحتوي على 1g هيدروجين و 19g أكسجين، النسبة المئوية للهيدروجين =",
                options: ["1%", "5%", "95%"],
                correct: 1
            },
            {
                section: "إضافات عامة",
                question: "أيّ من الخواص التالية لا يمكن ملاحظتها مباشرة؟",
                options: ["الكثافة", "اللون", "الشكل"],
                correct: 0
            },
            {
                section: "إضافات عامة",
                question: "أيّ من التغيرات التالية لا يُعدّ كيميائيًا؟",
                options: ["التبخر", "الاحتراق", "الصدأ"],
                correct: 0
            },
            {
                section: "إضافات عامة",
                question: "عند تفاعل الحديد مع الكبريت لتكوين كبريتيد الحديد يحدث:",
                options: ["تغير فيزيائي", "تغير كيميائي", "لا تغير"],
                correct: 1
            },
            {
                section: "إضافات عامة",
                question: "أيّ مما يلي يُعتبر تغيرًا فيزيائيًا عكسيًا؟",
                options: ["ذوبان الثلج", "احتراق الفحم", "صدأ الحديد"],
                correct: 0
            },
            {
                section: "إضافات عامة",
                question: "الخاصية التي تحدد قدرة المادة على التفاعل مع الأحماض:",
                options: ["كيميائية", "فيزيائية", "ممتدة"],
                correct: 0
            },
            {
                section: "إضافات عامة",
                question: "أي من الحالات التالية لها جسيمات متقاربة جدًا؟",
                options: ["الصلب", "السائل", "الغاز"],
                correct: 0
            },
            {
                section: "إضافات عامة",
                question: "أي من الحالات التالية لها جسيمات متباعدة جدًا؟",
                options: ["الصلب", "السائل", "الغاز"],
                correct: 2
            }
        ];

        // متغيرات التطبيق
        let currentQuestion = 0;
        let userAnswers = new Array(questions.length).fill(null);
        let score = 0;

        // عناصر DOM
        const introElement = document.querySelector('.intro');
        const quizContainer = document.getElementById('quiz-container');
        const questionSection = document.getElementById('question-section');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const startBtn = document.getElementById('start-btn');
        const resultsElement = document.getElementById('results');
        const scoreElement = document.getElementById('score');
        const resultMessage = document.getElementById('result-message');
        const restartBtn = document.getElementById('restart-btn');
        const progressElement = document.getElementById('progress');

        // بدء الاختبار
        startBtn.addEventListener('click', startQuiz);

        function startQuiz() {
            introElement.style.display = 'none';
            quizContainer.style.display = 'block';
            showQuestion();
        }

        // عرض السؤال الحالي
        function showQuestion() {
            const question = questions[currentQuestion];
            
            // تحديث شريط التقدم
            progressElement.style.width = `${((currentQuestion + 1) / questions.length) * 100}%`;
            
            // عرض عنوان القسم إذا تغير
            let sectionHTML = '';
            if (currentQuestion === 0 || questions[currentQuestion].section !== questions[currentQuestion - 1].section) {
                sectionHTML = `<div class="section-title">${question.section}</div>`;
            }
            
            // إنشاء HTML للسؤال
            let questionHTML = `
                ${sectionHTML}
                <div class="question-number">سؤال ${currentQuestion + 1} من ${questions.length}</div>
                <div class="question-text">${question.question}</div>
                <div class="options">
            `;
            
            question.options.forEach((option, index) => {
                const isSelected = userAnswers[currentQuestion] === index;
                questionHTML += `
                    <div class="option ${isSelected ? 'selected' : ''}" data-index="${index}">
                        <input type="radio" id="option-${index}" name="answer" ${isSelected ? 'checked' : ''}>
                        <label for="option-${index}">${option}</label>
                    </div>
                `;
            });
            
            questionHTML += `</div>`;
            questionSection.innerHTML = questionHTML;
            
            // إضافة مستمعي الأحداث للخيارات
            document.querySelectorAll('.option').forEach(option => {
                option.addEventListener('click', selectOption);
            });
            
            // تحديث حالة الأزرار
            prevBtn.disabled = currentQuestion === 0;
            nextBtn.textContent = currentQuestion === questions.length - 1 ? 'إنهاء الاختبار' : 'التالي';
        }

        // اختيار إجابة
        function selectOption(e) {
            const selectedOption = e.currentTarget;
            const selectedIndex = parseInt(selectedOption.getAttribute('data-index'));
            
            // إزالة التحديد من جميع الخيارات
            document.querySelectorAll('.option').forEach(option => {
                option.classList.remove('selected');
            });
            
            // تحديد الخيار المختار
            selectedOption.classList.add('selected');
            
            // حفظ إجابة المستخدم
            userAnswers[currentQuestion] = selectedIndex;
        }

        // الانتقال إلى السؤال التالي
        nextBtn.addEventListener('click', nextQuestion);

        function nextQuestion() {
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                showQuestion();
            } else {
                finishQuiz();
            }
        }

        // الانتقال إلى السؤال السابق
        prevBtn.addEventListener('click', () => {
            if (currentQuestion > 0) {
                currentQuestion--;
                showQuestion();
            }
        });

        // إنهاء الاختبار وعرض النتائج
        function finishQuiz() {
            // حساب النتيجة
            score = 0;
            userAnswers.forEach((answer, index) => {
                if (answer === questions[index].correct) {
                    score++;
                }
            });
            
            // عرض النتائج
            quizContainer.style.display = 'none';
            resultsElement.style.display = 'block';
            scoreElement.textContent = `${score}/${questions.length}`;
            
            // رسالة التقييم
            let message = '';
            const percentage = (score / questions.length) * 100;
            
            if (percentage >= 90) {
                message = 'ممتاز! لديك فهم رائع لخواص المادة.';
            } else if (percentage >= 70) {
                message = 'جيد جدًا! لديك معرفة جيدة بموضوع خواص المادة.';
            } else if (percentage >= 50) {
                message = 'مقبول، لكن يمكنك تحسين معرفتك بخواص المادة.';
            } else {
                message = 'يحتاج إلى تحسين. ننصحك بمراجعة موضوع خواص المادة.';
            }
            
            resultMessage.textContent = message;
        }

        // إعادة الاختبار
        restartBtn.addEventListener('click', () => {
            currentQuestion = 0;
            userAnswers = new Array(questions.length).fill(null);
            score = 0;
            
            resultsElement.style.display = 'none';
            quizContainer.style.display = 'block';
            showQuestion();
        });
    </script>
</body>
</html>
