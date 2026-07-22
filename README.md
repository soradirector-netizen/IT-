<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>民事法 テスト対策学習アプリ</title>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --success-color: #2ecc71;
            --danger-color: #e74c3c;
            --warning-color: #f1c40f;
            --bg-color: #f8f9fa;
            --card-bg: #ffffff;
        }

        body {
            font-family: 'Helvetica Neue', Arial, 'Hiragino Kaku Gothic ProN', 'Hiragino Sans', Meiryo, sans-serif;
            background-color: var(--bg-color);
            color: #333;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
        }

        .container {
            width: 100%;
            max-width: 800px;
            background: var(--card-bg);
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        h1, h2, h3 {
            color: var(--primary-color);
            text-align: center;
        }

        .btn {
            background-color: var(--secondary-color);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.2s, transform 0.1s;
            margin: 5px;
        }

        .btn:hover { background-color: #2980b9; }
        .btn:active { transform: scale(0.98); }
        .btn-success { background-color: var(--success-color); }
        .btn-success:hover { background-color: #27ae60; }
        .btn-warning { background-color: var(--warning-color); color: #333; }
        .btn-danger { background-color: var(--danger-color); }
        .btn-outline { background-color: transparent; color: var(--secondary-color); border: 2px solid var(--secondary-color); }
        .btn-outline.active { background-color: var(--secondary-color); color: white; }

        .hidden { display: none !important; }

        /* モード選択画面 */
        .mode-selection {
            display: flex;
            flex-direction: column;
            gap: 20px;
            margin-top: 30px;
        }

        .mode-card {
            border: 2px solid #e0e0e0;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
        }

        .mode-card:hover {
            border-color: var(--secondary-color);
            background-color: #f0f8ff;
        }

        .user-name-area {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            align-items: center;
            gap: 10px;
            margin-bottom: 20px;
            text-align: center;
        }

        .user-name-area input[type="text"] {
            flex: 1;
            min-width: 220px;
            padding: 10px;
            border: 2px solid #ccc;
            border-radius: 6px;
            font-size: 16px;
        }

        .ranking-section {
            border: 1px solid #e2e8f0;
            padding: 20px;
            border-radius: 8px;
            background-color: #fff;
            margin-top: 20px;
        }

        .ranking-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }

        .ranking-table th,
        .ranking-table td {
            border: 1px solid #e2e8f0;
            padding: 10px;
            text-align: center;
            font-size: 14px;
        }

        .ranking-table th {
            background-color: #f0f4f8;
        }

        .ranking-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 10px;
            flex-wrap: wrap;
        }

        .current-user-label {
            font-weight: bold;
            color: var(--secondary-color);
        }

        /* コントロールパネル */
        .control-panel {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            background: #edf2f7;
            padding: 12px 20px;
            border-radius: 8px;
            margin-bottom: 20px;
        }

        .question-card {
            border: 1px solid #e2e8f0;
            padding: 20px;
            border-radius: 8px;
            background-color: #fff;
            margin-bottom: 20px;
        }

        .tag {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 12px;
            font-weight: bold;
            margin-right: 5px;
        }

        .tag-past { background-color: #ffeaa7; color: #d63031; }
        .tag-category { background-color: #dfe6e9; color: #2d3436; }

        .bookmark-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #ccc;
            float: right;
        }

        .bookmark-btn.active { color: var(--warning-color); }

        /* 回答エリア */
        .input-group {
            margin: 20px 0;
            display: flex;
            gap: 10px;
        }

        .input-group input[type="text"] {
            flex: 1;
            padding: 10px;
            font-size: 16px;
            border: 2px solid #ccc;
            border-radius: 6px;
        }

        .options-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 10px;
            margin: 20px 0;
        }

        .option-btn {
            background-color: #fff;
            border: 2px solid #e2e8f0;
            padding: 12px 20px;
            border-radius: 8px;
            text-align: left;
            font-size: 15px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .option-btn:hover {
            border-color: var(--secondary-color);
            background-color: #f7fafc;
        }

        /* 判定・解説表示 */
        .feedback {
            padding: 15px;
            border-radius: 6px;
            margin-top: 15px;
        }

        .feedback.correct { background-color: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
        .feedback.incorrect { background-color: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }

        .article-box {
            background-color: #f1f5f9;
            border-left: 4px solid var(--secondary-color);
            padding: 10px 15px;
            margin-top: 10px;
            font-size: 14px;
            white-space: pre-wrap;
        }

        .nav-btns {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>民事法 学習システム</h1>

    <!-- 1. モード選択画面 -->
    <div id="mode-select-screen">
        <h2>学習モードを選択してください</h2>
        <div class="user-name-area">
            <label for="user-name-input">ユーザー名:</label>
            <input type="text" id="user-name-input" placeholder="お名前を入力してください">
            <button class="btn btn-outline" onclick="saveUserName()">保存</button>
            <span id="current-user-label" class="current-user-label"></span>
        </div>
        <div style="text-align: center; margin-bottom: 10px;">
            <button class="btn btn-outline" onclick="showRanking()">ランキングを見る</button>
        </div>
        <div class="mode-selection">
            <div class="mode-card" onclick="selectMode(1)">
                <h3>例１：空所補充記述問題</h3>
                <p>重要用語言語を直接記述して回答するモードです。（全145問）</p>
            </div>
            <div class="mode-card" onclick="selectMode(2)">
                <h3>例２：シチュエーション問題（条文選択）</h3>
                <p>設例に対応する民法条文を4つの選択肢から選ぶモードです。（全54問）</p>
            </div>
        </div>
    </div>

    <!-- 2. メイン問題画面 -->
    <div id="quiz-screen" class="hidden">
        <div class="control-panel">
            <div>
                <span id="progress-text">問題 1 / 10</span>
                <button id="past-only-btn" class="btn btn-outline" onclick="togglePastOnly()">過去問のみ</button>
                <button class="btn btn-outline" onclick="shuffleQuestions()">🔀 問題シャッフル</button>
            </div>
            <div>
                <button class="btn btn-warning" onclick="switchModeSelect()">モード切替</button>
            </div>
        </div>

        <div class="question-card">
            <button id="bookmark-toggle" class="bookmark-btn" onclick="toggleBookmark()">★</button>
            <div style="margin-bottom: 10px;">
                <span id="past-tag" class="tag tag-past hidden">★ 過去問</span>
                <span id="category-tag" class="tag tag-category">カテゴリ</span>
            </div>
            
            <h3 id="question-title">問1</h3>
            <div id="question-text" style="font-size: 17px; line-height: 1.6; margin-bottom: 15px;"></div>

            <!-- 例1 用入力フォーム -->
            <div id="mode1-input" class="input-group hidden">
                <input type="text" id="type-answer" placeholder="解答を入力してください"
                    onkeydown="if (event.key === 'Enter') { event.preventDefault(); return false; }">
                <button class="btn btn-success" onclick="checkAnswerMode1()">回答する</button>
            </div>

            <!-- 例2 用選択肢 -->
            <div id="mode2-options" class="options-grid hidden"></div>

            <!-- フィードバック表示エリア -->
            <div id="feedback-area" class="feedback hidden"></div>
        </div>

        <div class="nav-btns">
            <button class="btn" onclick="prevQuestion()">← 前の問題</button>
            <button class="btn btn-success" onclick="finishQuiz()">採点・結果を見る</button>
            <button class="btn" onclick="nextQuestion()">次の問題 →</button>
        </div>
    </div>

    <div id="ranking-section" class="ranking-section hidden">
        <div class="ranking-header">
            <h2>ランキング</h2>
            <button class="btn btn-outline" onclick="closeRanking()">閉じる</button>
        </div>
        <p>例1・例2の正答数の合計で順位付けされます。最新のスコアが反映されます。</p>
        <table class="ranking-table">
            <thead>
                <tr>
                    <th>順位</th>
                    <th>ユーザー名</th>
                    <th>例1 正答数</th>
                    <th>例2 正答数</th>
                    <th>合計</th>
                </tr>
            </thead>
            <tbody id="ranking-table-body"></tbody>
        </table>
    </div>

    <!-- 3. 結果画面 -->
    <div id="result-screen" class="hidden">
        <h2>採点結果</h2>
        <div style="text-align: center; margin: 30px 0;">
            <p style="font-size: 24px;">正解率: <strong id="score-percentage" style="font-size: 36px; color: var(--secondary-color);">0%</strong></p>
            <p id="score-detail" style="font-size: 18px; color: #666;"></p>
        </div>
        <div style="display: flex; justify-content: center; gap: 10px; flex-wrap: wrap;">
            <button class="btn btn-danger" id="retry-mistakes-btn" onclick="retryMistakesOrBookmarks()">間違えた問題＋苦手問題をまとめて復習</button>
            <button class="btn btn-success" onclick="restartQuiz()">最初からやり直す</button>
            <button class="btn btn-warning" onclick="switchModeSelect()">モード選択に戻る</button>
        </div>
    </div>
</div>

<script>
// --- データ定義 ---

// 例1（空所補充）問題データ
const rawDataMode1 = [
    { id: 1, cat: "第1回 民法の位置付け", past: false, text: "私人間の財産や親族・相続をめぐる生活関係を規律する私法であり、私人間の紛争解決の基準となる実体法・一般法を（a）という。", ans: ["民法"] },
    { id: 2, cat: "第1回 民法の位置付け", past: false, text: "国または地方公共団体に対する国民または住民としての生活関係を規律する法を（a）という。", ans: ["公法"] },
    { id: 3, cat: "第1回 民法の位置付け", past: false, text: "財産や親族・相続をめぐる私人間の生活関係を規律する法を（a）という。", ans: ["私法"] },
    { id: 4, cat: "第1回 民法の位置付け", past: false, text: "裁判をする際の紛争解決の基準となる法を（a）という。", ans: ["実体法"] },
    { id: 5, cat: "第1回 民法の位置付け", past: false, text: "文書で定められた法規範（制定法）を（a）という。", ans: ["成文法"] },
    { id: 6, cat: "第1回 民法の位置付け", past: false, text: "法的拘束力を持つ慣習を（a）という。", ans: ["慣習法"] },
    { id: 7, cat: "第1回 民法の位置付け", past: true, text: "人は自らの意思によって自由に財産関係を創出することができるという原則を（a）という。", ans: ["私的自治の原則"] },
    { id: 8, cat: "第1回 民法の位置付け", past: true, text: "所有者は法令の制限内で自由にその所有物を使用・収益・処分できるという原則を（a）という。", ans: ["所有権絶対の原則"] },
    { id: 9, cat: "第1回 民法の位置付け", past: true, text: "契約を締結するか、内容をどのように決めるか、どの方式で契約するかを自由に決定できる原則を（a）という。", ans: ["契約自由の原則"] },
    { id: 10, cat: "第1回 民法の位置付け", past: false, text: "故意または過失によって他人の権利・利益を侵害した者が損害賠償責任を負うという原則を（a）という。", ans: ["過失責任主義"] },
    { id: 11, cat: "第1回 民法の位置付け", past: false, text: "権利行使の外観を備えているが、実質的には権利行使の正当な範囲を超えることを（a）という。", ans: ["権利濫用"] },
    { id: 12, cat: "第1回 民法の位置付け", past: false, text: "公の秩序又は善良の風俗に反する法律行為は無効となる。この「公の秩序又は善良の風俗」を（a）という。", ans: ["公序良俗"] },
    
    { id: 13, cat: "第2回 民法総則", past: false, text: "ある事実を知らないことを（a）という。なお、道徳的な善悪とは無関係である。", ans: ["善意"] },
    { id: 14, cat: "第2回 民法総則", past: false, text: "ある事実を知っていることを（a）という。なお、道徳的な善悪とは無関係である。", ans: ["悪意"] },
    { id: 15, cat: "第2回 民法総則", past: false, text: "すでに効力の生じた法律関係を第三者に主張することを（a）という。", ans: ["対抗"] },
    { id: 16, cat: "第2回 民法総則", past: false, text: "法律行為が、何らかの理由により当事者の表示した効果意思の内容に従った法律上の効果を生じないことを（a）という。", ans: ["無効"] },
    { id: 17, cat: "第2回 民法総則", past: false, text: "法律行為の効力を当初に遡って失わせることを（a）という。", ans: ["取消し", "取消"] },
    { id: 18, cat: "第2回 民法総則", past: false, text: "申込みと承諾という二つの意思表示が合致（合意）することで成立する法律行為を（a）という。", ans: ["契約"] },
    { id: 19, cat: "第2回 民法総則", past: false, text: "契約の内容を示して締結を申し入れる意思表示を（a）という。", ans: ["申込み", "申込"] },
    { id: 20, cat: "第2回 民法総則", past: false, text: "申込みに対し契約を成立させる意思表示を（a）という。", ans: ["承諾"] },
    { id: 21, cat: "第2回 民法総則", past: false, text: "特定の人に対して一定の行為を請求する権利を（a）という。", ans: ["債権"] },
    { id: 22, cat: "第2回 民法総則", past: false, text: "債権に対応して一定の行為をしなければならない義務を（a）という。", ans: ["債務"] },
    { id: 23, cat: "第2回 民法総則", past: false, text: "物を直接支配する権利であり、絶対権・排他的権利・一物一権主義という特徴をもつものを（a）という。", ans: ["物権"] },
    { id: 24, cat: "第2回 民法総則", past: false, text: "物権は法律で定められた種類しか認められないという原則を（a）という。", ans: ["物権法定主義"] },
    { id: 25, cat: "第2回 民法総則", past: false, text: "権利を取得し義務を負うことのできる資格を（a）という。", ans: ["権利能力"] },
    { id: 26, cat: "第2回 民法総則", past: false, text: "判断能力の不十分な者を保護する制度を（a）という。", ans: ["制限行為能力"] },
    { id: 27, cat: "第2回 民法総則", past: true, text: "未成年者、成年被後見人、被保佐人、被補助人の総称を（a）という。", ans: ["制限行為能力者"] },

    { id: 28, cat: "第3回 民法総則（意思表示）", past: true, text: "一定の私権の変動（法律効果の発生）を欲する意思を外部に表示することを（a）という。", ans: ["意思表示"] },
    { id: 29, cat: "第3回 民法総則（意思表示）", past: true, text: "二つの対立する意思表示が合致（合意）することによって成立する法律行為を（a）という。", ans: ["契約"] },
    { id: 30, cat: "第3回 民法総則（意思表示）", past: false, text: "意思表示は、その通知が相手方に到達した時から効力を生ずるという原則を（a）という。", ans: ["到達主義"] },
    { id: 31, cat: "第3回 民法総則（意思表示）", past: false, text: "意思表示によって法律効果を発生させる行為を（a）という。", ans: ["法律行為"] },
    { id: 32, cat: "第3回 民法総則（意思表示）", past: true, text: "内心の効果意思と表示との不一致があり、それを表意者が知っている場合を（a）という。", ans: ["心裡留保"] },
    { id: 33, cat: "第3回 民法総則（意思表示）", past: true, text: "相手方と通じてした虚偽の意思表示を（a）という。", ans: ["虚偽表示"] },
    { id: 34, cat: "第3回 民法総則（意思表示）", past: true, text: "事実と異なる認識に基づいて意思表示をすることを（a）という。", ans: ["錯誤"] },
    { id: 35, cat: "第3回 民法総則（意思表示）", past: false, text: "法律行為の基礎とした事情について認識が真実に反する錯誤を（a）という。", ans: ["動機錯誤", "動機の錯誤"] },
    { id: 36, cat: "第3回 民法総則（意思表示）", past: true, text: "欺罔して相手方を錯誤に陥れる行為を（a）という。", ans: ["詐欺"] },
    { id: 37, cat: "第3回 民法総則（意思表示）", past: true, text: "害悪を告知して相手方を畏怖させ、それによって意思表示をさせることを（a）という。", ans: ["強迫"] },
    { id: 38, cat: "第3回 民法総則（意思表示）", past: true, text: "何らの行為を要せず当然に効力を生じないことを（a）という。", ans: ["無効"] },
    { id: 39, cat: "第3回 民法総則（意思表示）", past: true, text: "取消権者が取り消すことで初めて遡って無効となることを（a）という。", ans: ["取消し", "取消"] },
    { id: 40, cat: "第3回 民法総則（意思表示）", past: false, text: "取り消すことのできる法律行為を、その後確定的に有効とする意思表示を（a）という。", ans: ["追認"] },

    { id: 41, cat: "第4回 民法総則（代理等）", past: true, text: "本人に代わって代理人が意思表示をし、その法律効果が本人に直接帰属する制度を（a）という。", ans: ["代理"] },
    { id: 42, cat: "第4回 民法総則（代理等）", past: true, text: "本人が代理人に代理権を与えることを（a）という。", ans: ["授権"] },
    { id: 43, cat: "第4回 民法総則（代理等）", past: true, text: "代理人が本人のためにすることを示して意思表示をすることを（a）という。", ans: ["顕名"] },
    { id: 44, cat: "第4回 民法総則（代理等）", past: true, text: "代理権がないにもかかわらず代理人としてした行為を（a）という。", ans: ["無権代理"] },
    { id: 45, cat: "第4回 民法総則（代理等）", past: true, text: "代理権がないにもかかわらず、代理権があるように見える場合に善意の第三者を保護する制度を（a）という。", ans: ["表見代理"] },
    { id: 46, cat: "第4回 民法総則（代理等）", past: false, text: "法律行為の効力の発生又は消滅を、将来発生するかどうか不確実な事実にかからせる附款を（a）という。", ans: ["条件"] },
    { id: 47, cat: "第4回 民法総則（代理等）", past: false, text: "条件が成就したときに効力が発生する条件を（a）という。", ans: ["停止条件"] },
    { id: 48, cat: "第4回 民法総則（代理等）", past: false, text: "条件が成就したときに効力が消滅する条件を（a）という。", ans: ["解除条件"] },
    { id: 49, cat: "第4回 民法総則（代理等）", past: false, text: "一定期間権利を行使しないことにより権利が消滅する制度を（a）という。", ans: ["消滅時効"] },
    { id: 50, cat: "第4回 民法総則（代理等）", past: false, text: "一定期間占有することによって権利を取得する制度を（a）という。", ans: ["取得時効"] },
    { id: 51, cat: "第4回 民法総則（代理等）", past: false, text: "時効期間がリセットされ、新たに進行することを（a）という。", ans: ["時効の更新"] },
    { id: 52, cat: "第4回 民法総則（代理等）", past: false, text: "一定期間、時効の完成を猶予する制度を（a）という。", ans: ["時効の完成猶予"] },

    { id: 53, cat: "第5回 債権総論・契約総論", past: true, text: "特定の人（債務者）に対して一定の行為（給付）を請求することができる権利を（a）という。", ans: ["債権"] },
    { id: 54, cat: "第5回 債権総論・契約総論", past: true, text: "債権に対応して、一定の給付をしなければならない義務を（a）という。", ans: ["債務"] },
    { id: 55, cat: "第5回 債権総論・契約総論", past: true, text: "申込みと承諾という意思表示が合致することによって成立する法律行為を（a）という。", ans: ["契約"] },
    { id: 56, cat: "第5回 債権総論・契約総論", past: true, text: "当事者が自由に契約を締結し、その内容・相手方・方式を決定できるという原則を（a）という。", ans: ["契約自由の原則"] },
    { id: 57, cat: "第5回 債権総論・契約総論", past: false, text: "双方が互いに債務を負う契約を（a）という。", ans: ["双務契約"] },
    { id: 58, cat: "第5回 債権総論・契約総論", past: true, text: "双務契約において、相手方が履行を提供するまでは、自分も履行を拒むことができる権利を（a）という。", ans: ["同時履行の抗弁権"] },
    { id: 59, cat: "第5回 債権総論・契約総論", past: true, text: "履行期を過ぎても履行しないことを（a）という。", ans: ["履行遅滞"] },
    { id: 60, cat: "第5回 債権総論・契約総論", past: true, text: "債務の履行が不可能となることを（a）という。", ans: ["履行不能"] },
    { id: 61, cat: "第5回 債権総論・契約総論", past: true, text: "債務者が債務の内容どおりに履行しないことを（a）という。", ans: ["債務不履行"] },
    { id: 62, cat: "第5回 債権総論・契約総論", past: true, text: "契約を将来に向かって消滅させることを（a）という。", ans: ["契約解除"] },

    { id: 63, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "特定の人に対して一定の行為（給付）を請求することができる権利を（a）という。", ans: ["債権"] },
    { id: 64, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "一定の給付をしなければならない義務を（a）という。", ans: ["債務"] },
    { id: 65, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "債権を消滅させる行為を（a）という。", ans: ["弁済"] },
    { id: 66, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "債務を履行すべき時期を（a）という。", ans: ["弁済期"] },
    { id: 67, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "債務者が自分のできる行為を行って債権者の協力を促すことを（a）という。", ans: ["弁済の提供"] },
    { id: 68, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "双務契約において、「相手方が債務を履行しないうちは、自分も履行しない」と主張できる権利を（a）という。", ans: ["同時履行の抗弁権"] },
    { id: 69, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "双方の債務が互いに対応し合う関係を（a）という。", ans: ["牽連性"] },
    { id: 70, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "債務者が債務の本旨に従った履行をしない場合に負う責任を（a）という。", ans: ["債務不履行責任"] },
    { id: 71, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "履行できるにもかかわらず、弁済期を過ぎても履行しないことを（a）という。", ans: ["履行遅滞"] },
    { id: 72, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "債務の履行が不能となることを（a）という。", ans: ["履行不能"] },
    { id: 73, cat: "第6回 情報契約法（契約の効力等）", past: true, text: "履行はされたが、その内容が不完全であることを（a）という。", ans: ["不完全履行"] },

    { id: 74, cat: "第7回 契約不適合責任等", past: true, text: "売買契約で、給付されたものが契約内容に適合しない「不完全履行」の場合について、一般の債務不履行責任の特則として売主が負う責任を（a）という。", ans: ["契約不適合責任"] },
    { id: 75, cat: "第7回 契約不適合責任等", past: true, text: "一応の履行はされたが、その履行内容が契約内容に適合していないことを（a）という。", ans: ["不完全履行"] },
    { id: 76, cat: "第7回 契約不適合責任等", past: true, text: "買主が売主に対して、目的物の修補・代替物の引渡し・不足分の引渡しを請求できる権利を（a）という。", ans: ["追完請求権"] },
    { id: 77, cat: "第7回 契約不適合責任等", past: true, text: "売主が追完しない場合に、不適合の程度に応じて代金の減額を請求できる権利を（a）という。", ans: ["代金減額請求権"] },
    { id: 78, cat: "第7回 契約不適合責任等", past: false, text: "契約内容に適合するように、目的物を修理することを（a）という。", ans: ["修補"] },
    { id: 79, cat: "第7回 契約不適合責任等", past: false, text: "契約内容に適合した別の物を引き渡すことを（a）という。", ans: ["代替物の引渡し"] },
    { id: 80, cat: "第7回 契約不適合責任等", past: false, text: "不足している数量を追加して引き渡すことを（a）という。", ans: ["不足分の引渡し"] },
    { id: 81, cat: "第7回 契約不適合責任等", past: true, text: "種類・品質に関する契約不適合を知った時から1年以内に通知しなければ権利行使できない。この期間を（a）という。", ans: ["権利行使期間"] },
    { id: 82, cat: "第7回 契約不適合責任等", past: true, text: "契約を解消し、自分の履行義務を免れる制度を（a）という。", ans: ["契約解除"] },
    { id: 83, cat: "第7回 契約不適合責任等", past: false, text: "法律により認められる解除権を（a）という。", ans: ["法定解除権"] },
    { id: 84, cat: "第7回 契約不適合責任等", past: false, text: "契約であらかじめ定める解除権を（a）という。", ans: ["約定解除権"] },
    { id: 85, cat: "第7回 契約不適合責任等", past: true, text: "相当期間を定めて履行を求めることを（a）という。", ans: ["催告"] },
    { id: 86, cat: "第7回 契約不適合責任等", past: true, text: "契約を解除した場合に、各当事者が相手方を元の状態に戻す義務を（a）という。", ans: ["原状回復義務"] },

    { id: 87, cat: "第8回 典型契約", past: false, text: "民法が名称・内容を定めている契約を（a）という。", ans: ["典型契約"] },
    { id: 88, cat: "第8回 典型契約", past: true, text: "売主が財産権を相手方に移転し、それに対して買主が代金を支払うことを約束する契約を（a）という。", ans: ["売買"] },
    { id: 89, cat: "第8回 典型契約", past: false, text: "当事者の一方が無償で財産を与え、相手方が受諾する契約を（a）という。", ans: ["贈与"] },
    { id: 90, cat: "第8回 典型契約", past: true, text: "借主が貸主から受け取った物と同じ種類・品質・数量の物を返還することを約束して成立する契約を（a）という。", ans: ["消費貸借"] },
    { id: 91, cat: "第8回 典型契約", past: true, text: "貸主が金銭その他の物を引き渡すことを約し、借主が返還を書面で約束する契約を（a）という。", ans: ["書面による消費貸借"] },
    { id: 92, cat: "第8回 典型契約", past: false, text: "目的物を無償で使用・収益し、契約終了後に返還する契約を（a）という。", ans: ["使用貸借"] },
    { id: 93, cat: "第8回 典型契約", past: false, text: "賃貸人が目的物を使用・収益させ、賃借人が賃料を支払い、契約終了後に返還する契約を（a）という。", ans: ["賃貸借"] },
    { id: 94, cat: "第8回 典型契約", past: true, text: "建物所有を目的とする土地・建物の賃貸借について、賃借人を保護する特別法を（a）という。", ans: ["借地借家法"] },
    { id: 95, cat: "第8回 典型契約", past: true, text: "請負人が仕事を完成することを約束し、注文者がその結果に対して報酬を支払う契約を（a）という。", ans: ["請負"] },
    { id: 96, cat: "第8回 典型契約", past: false, text: "委任者が法律行為をすることを受任者に委託し、受任者が承諾することで成立する契約を（a）という。", ans: ["委任"] },
    { id: 97, cat: "第8回 典型契約", past: false, text: "委任を受けて事務を処理する者を（a）という。", ans: ["受任者"] },
    { id: 98, cat: "第8回 典型契約", past: false, text: "委任する者を（a）という。", ans: ["委任者"] },
    { id: 99, cat: "第8回 典型契約", past: true, text: "善良な管理者として通常要求される注意義務を（a）という。", ans: ["善管注意義務"] },

    { id: 101, cat: "第9回 約款・消費者保護法", past: true, text: "当事者が自由な意思で契約を締結し、その内容・方式などを自由に決定できるという原則を（a）という。", ans: ["契約自由の原則"] },
    { id: 102, cat: "第9回 約款・消費者保護法", past: true, text: "不特定多数の者を相手方として画一的に契約内容を定める約款を（a）という。", ans: ["定型約款"] },
    { id: 103, cat: "第9回 約款・消費者保護法", past: false, text: "相手方の利益を一方的に害する条項は契約内容にならない。この制度を（a）という。", ans: ["定型約款の無効"] },
    { id: 104, cat: "第9回 約款・消費者保護法", past: false, text: "一定の場合には相手方の同意がなくても定型約款を変更できる制度を（a）という。", ans: ["定型約款の変更"] },
    { id: 105, cat: "第9回 約款・消費者保護法", past: true, text: "事業者と消費者との契約について、民法の一般原則を修正して消費者を保護する法律を（a）という。", ans: ["消費者契約法"] },
    { id: 106, cat: "第9回 約款・消費者保護法", past: false, text: "事業者が不適切な勧誘をした場合に、消費者が契約を取り消すことができる制度を（a）という。", ans: ["意思表示の取消し", "意思表示の取消"] },
    { id: 107, cat: "第9回 約款・消費者保護法", past: false, text: "消費者の利益を一方的に害する契約条項は無効となる。この制度を（a）という。", ans: ["契約条項の無効"] },
    { id: 108, cat: "第9回 約款・消費者保護法", past: false, text: "適格消費者団体が不当な勧誘や契約条項の差止めを請求できる制度を（a）という。", ans: ["消費者団体訴権制度"] },
    { id: 109, cat: "第9回 約款・消費者保護法", past: false, text: "多数の消費者被害について、集団的な被害回復を図るための裁判手続を定めた法律を（a）という。", ans: ["消費者裁判手続特例法"] },
    { id: 110, cat: "第9回 約款・消費者保護法", past: true, text: "分割払いによる販売を規制し、消費者を保護する法律を（a）という。", ans: ["割賦販売法"] },
    { id: 111, cat: "第9回 約款・消費者保護法", past: true, text: "訪問販売・通信販売などを規制し、消費者を保護する法律を（a）という。", ans: ["特定商取引法"] },
    { id: 112, cat: "第9回 約款・消費者保護法", past: false, text: "一定期間内であれば無条件で契約を解除できる制度を（a）という。", ans: ["クーリング・オフ制度", "クーリングオフ制度", "クーリング・オフ"] },

    { id: 113, cat: "第10回 電子商取引法", past: false, text: "インターネット等を利用して商品やサービスの売買・契約を行う取引を（a）という。", ans: ["電子商取引"] },
    { id: 114, cat: "第10回 電子商取引法", past: false, text: "コンピュータ・ネットワークを介して申込み・承諾を行う契約を（a）という。", ans: ["オンライン契約"] },
    { id: 115, cat: "第10回 電子商取引法", past: false, text: "AIスピーカーを利用して商品やサービスの売買・契約を行う取引を（a）という。", ans: ["AIスピーカーによる契約"] },
    { id: 116, cat: "第10回 電子商取引法", past: false, text: "本人が注文する意思を有していない場合には契約は成立しない。このようなAIスピーカーの問題を（a）という。", ans: ["AIスピーカーの誤認識"] },
    { id: 117, cat: "第10回 電子商取引法", past: false, text: "現時点では法律上認められていない、AIに与える法的地位を（a）という。", ans: ["法人格"] },
    { id: 118, cat: "第10回 電子商取引法", past: false, text: "現在のAIスピーカーについては、ユーザーの（a）とは解釈されない。", ans: ["代理人"] },
    { id: 119, cat: "第10回 電子商取引法", past: false, text: "意思表示に誤りがあることを（a）という。", ans: ["錯誤"] },
    { id: 120, cat: "第10回 電子商取引法", past: false, text: "言い間違い・書き間違いによる錯誤を（a）という。", ans: ["表示錯誤"] },
    { id: 121, cat: "第10回 電子商取引法", past: false, text: "思い違いによる錯誤を（a）という。", ans: ["内容錯誤"] },
    { id: 122, cat: "第10回 電子商取引法", past: false, text: "法律行為の基礎事情について認識を誤った錯誤を（a）という。", ans: ["動機錯誤", "動機の錯誤"] },
    { id: 123, cat: "第10回 電子商取引法", past: false, text: "重要な錯誤がある場合に意思表示を取り消すことを（a）という。", ans: ["錯誤取消し", "錯誤取消"] },
    { id: 124, cat: "第10回 電子商取引法", past: false, text: "重大な過失がある場合には、原則として錯誤による取消しは認められない。この重大な過失を（a）という。", ans: ["重過失"] },
    { id: 125, cat: "第10回 電子商取引法", past: true, text: "電子契約における消費者の操作ミスについて、民法95条3項の特例を定める法律を（a）という。", ans: ["電子消費者契約法"] },
    { id: 126, cat: "第10回 電子商取引法", past: true, text: "消費者のクリックミスなどについて、民法95条3項を適用しないと定める規定を（a）という。", ans: ["電子消費者契約法3条", "電子消費者契約法第3条"] },
    { id: 127, cat: "第10回 電子商取引法", past: false, text: "日本の消費者が外国事業者と行う電子取引を（a）という。", ans: ["国際取引"] },
    { id: 128, cat: "第10回 電子商取引法", past: false, text: "国際的な民事事件について、どの国の裁判所が裁判を行うかを定める制度を（a）という。", ans: ["国際裁判管轄"] },
    { id: 129, cat: "第10回 電子商取引法", past: false, text: "消費者契約では原則として無効となる、国際裁判管轄についてあらかじめ定める合意を（a）という。", ans: ["国際裁判管轄の事前合意"] },
    { id: 130, cat: "第10回 電子商取引法", past: false, text: "国際取引でどの国の法律を適用するかを定める法を（a）という。", ans: ["準拠法"] },

    { id: 131, cat: "第11回 大陸法・英米法", past: true, text: "ローマ法の流れをくむヨーロッパ大陸の法で、市民法（Civil Law）とも呼ばれる法体系を（a）という。", ans: ["大陸法", "大陸法（Civil Law）"] },
    { id: 132, cat: "第11回 大陸法・英米法", past: false, text: "大陸法では、裁判官は制定法に拘束され、判例は法源とされない。この考え方を（a）という。", ans: ["制定法主義", "成文法主義", "制定法（成文法）主義"] },
    { id: 133, cat: "第11回 大陸法・英米法", past: true, text: "一般的な成文法を個別事件に当てはめる考え方を（a）という。", ans: ["抽象的・演繹的思考"] },
    { id: 134, cat: "第11回 大陸法・英米法", past: false, text: "イギリス法を母法として発展した法体系を（a）という。", ans: ["英米法", "英米法（Common Law）"] },
    { id: 135, cat: "第11回 大陸法・英米法", past: true, text: "判例が第一次的な法源となる考え方を（a）という。", ans: ["判例法主義"] },
    { id: 136, cat: "第11回 大陸法・英米法", past: false, text: "裁判官が過去の判例（先例）に拘束される原則を（a）という。", ans: ["先例拘束性の原則"] },
    { id: 137, cat: "第11回 大陸法・英米法", past: false, text: "同種の事件を参考に結論を導く考え方を（a）という。", ans: ["具体的・帰納的思考"] },
    { id: 138, cat: "第11回 大陸法・英米法", past: false, text: "英米法において、先例のうち裁判所を拘束する判決理由を（a）という。", ans: ["レイシオ・デシデンダイ"] },
    { id: 139, cat: "第11回 大陸法・英米法", past: true, text: "英米法では契約成立のために意思の合致に加えて必要とされる、交換取引の存在を裏付けるものを（a）という。", ans: ["約因", "約因（Consideration）"] },
    { id: 140, cat: "第11回 大陸法・英米法", past: true, text: "契約書が存在する場合、契約書以外の口頭での約束は証拠として認めないという原則を（a）という。", ans: ["Parol Evidence Rule", "口頭証拠排除則", "Parol Evidence Rule（口頭証拠排除則）"] },
    { id: 141, cat: "第11回 大陸法・英米法", past: false, text: "本契約が完全な合意であり、それ以前の書面・口頭・黙示の合意は効力を失うと定める条項を（a）という。", ans: ["完全合意条項", "完全合意条項（Entire Agreement）"] },
    { id: 142, cat: "第11回 大陸法・英米法", past: false, text: "アメリカ法律協会（ALI）が判例法を整理して条文化したものを（a）という。", ans: ["Restatement", "リステイトメント", "Restatement（リステイトメント）"] },
    { id: 143, cat: "第11回 大陸法・英米法", past: false, text: "アメリカの商取引に関する統一法典を（a）という。", ans: ["UCC", "統一商事法典", "UCC（統一商事法典）"] },
    { id: 144, cat: "第11回 大陸法・英米法", past: false, text: "複数の国や地域の法制度を比較・研究する学問を（a）という。", ans: ["比較法"] },
    { id: 145, cat: "第11回 大陸法・英米法", past: false, text: "国家間の関係を規律する法を（a）という。", ans: ["国際法"] }
];

// 例2（シチュエーション問題）問題データ
const rawDataMode2 = [
    { id: 1, cat: "第1回 民法基本原理", past: false, article: "第92条", title: "慣習法", text: "〔設例〕AとBの取引において、法令中に公の秩序に関しない規定と異なる慣習が存在していた。当事者がその慣習による意思を有すると認められる場合に、その慣習が適用される根拠となる民法典の条数を【参考】条文から選択して答えよ。", content: "第92条 法令中の公の秩序に関しない規定と異なる慣習がある場合において、法律行為の当事者がその慣習による意思を有していたと認められるときは、その慣習に従う。" },
    { id: 2, cat: "第1回 民法基本原理", past: false, article: "第206条", title: "所有権絶対の原則", text: "〔設例〕Aは自己の所有する土地について、法令の制限内において自由にその所有物の使用、収益及び処分をする権利を有している。この所有権絶対の原則を定める民法典の条数を【参考】条文から選択して答えよ。", content: "第206条 所有者は、法令の制限内において、自由とその所有物の使用、収益及び処分をする権利を有する。" },
    { id: 3, cat: "第1回 民法基本原理", past: false, article: "第522条", title: "契約自由の原則", text: "〔設例〕AとBは、法律上の特別な定めがない契約において、書面を作成せず口頭での合意のみで契約を成立させた。契約の成立に原則として書面その他の方式を要しないとする根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第522条2項 契約の成立には、法令に特別の定めがある場合を除き、書面の作成その他の方式を具備することを要しない。" },
    { id: 4, cat: "第1回 民法基本原理", past: false, article: "第709条", title: "過失責任主義", text: "〔設例〕Aは不注意（過失）によってBの自動車に自分の自転車をぶつけ、損傷させた。故意または過失によって他人の権利や利益を侵害した者が損害賠償責任を負うとする根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第709条 故意又は過失によって他人の権利又は法律上保護される利益を侵害した者は、これによって生じた損害を賠償する責任を負う。" },
    { id: 5, cat: "第1回 民法基本原理", past: false, article: "第1条", title: "権利濫用", text: "〔設例〕Aは、宇奈月温泉の引湯管がわずかに自分の土地を無断通過していることを知り、土地を高額で買い取らせようとした。拒否されたため撤去訴訟を起こしたが認められなかった。根拠となる民法典の条数を【参考】条文から選択して答えよ。", content: "第1条3項 権利の濫用は、これを許さない。" },
    { id: 6, cat: "第1回 民法基本原理", past: false, article: "第90条", title: "公序良俗", text: "〔設例〕AはBとの間で、愛人関係を維持することを条件とする契約など社会規範に反する約束を交わした。公の秩序又は善良の風俗に反する法律行為を無効とする民法典の条数を【参考】条文から選択して答えよ。", content: "第90条 公の秩序又は善良の風俗に反する法律行為は、無効とする。" },
    { id: 7, cat: "第2回 民法総則", past: false, article: "第522条", title: "契約", text: "〔設例〕売主Aが「1000万円で売る」と申し込み、買主Bがそれを承諾した。申込みに対して相手方が承諾したときに契約が成立することを規定している民法典の条数を【参考】条文から選択して答えよ。", content: "第522条1項 契約は、契約の内容を示してされた一方の意思表示（申込み）に対して相手方が承諾をしたときに成立する。" },
    { id: 8, cat: "第2回 民法総則", past: false, article: "第249条", title: "共有", text: "〔設例〕AとBは1つの建物を共同で購入し、共有している。各共有者が共有物全部についてその持分に応じた使用をすることができる根拠となる民法典の条数を【参考】条文から選択して答えよ。", content: "第249条1項 各共有者は、共有物の全部について、その持分に応じた使用をすることができる。" },
    { id: 9, cat: "第2回 民法総則", past: false, article: "第180条", title: "占有権", text: "〔設例〕Aは自己のためにする意思をもって時計を事実上所持し、占有権を取得した。自己のためにする意思をもって物を所持することによって取得する権利について規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第180条 占有権は、自己のためにする意思をもって物を所持することによって取得する。" },
    { id: 10, cat: "第2回 民法総則", past: false, article: "第162条", title: "所有権取得時効", text: "〔設例〕Aは他人の土地であることを知りつつも、20年間所有の意思をもって平穏かつ公然に占有し続けた。この結果、Aが土地の所有権を取得する根拠となる民法典の条数を【参考】条文から選択して答えよ。", content: "第162条1項 二十年間、所有の意思をもって、平穏に、かつ、公然と他人の物を占有した者は、その所有権を取得する。" },
    { id: 11, cat: "第2回 民法総則", past: false, article: "第3条", title: "自然人の権利能力", text: "〔設例〕人は出生によって権利を取得し義務を負うことのできる資格を取得する。この自然人の権利能力の始期を定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第3条1項 私権の享受は、本人の出生に始まる。" },
    { id: 12, cat: "第2回 民法総則", past: false, article: "第3条の2", title: "意思能力", text: "〔設例〕Aは意思表示をした時に意思能力（自己の行為の結果を判断する精神的能力）を有していなかった。この場合、その法律行為が無効となる根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第3条の2 法律行為の当事者が意思表示をした時に意思能力を有しなかったときは、その法律行為は、無効とする。" },
    { id: 13, cat: "第2回 民法総則", past: false, article: "第86条", title: "不動産・動産", text: "〔設例〕土地及びその定着物は不動産であり、不動産以外の物はすべて動産とされる。不動産および動産の定義を定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第86条1項 土地及びその定着物は、不動産とする。 第86条2項 不動産以外の物は、すべて動産とする。" },
    { id: 14, cat: "第2回 民法総則", past: false, article: "第87条", title: "主物・従物", text: "〔設例〕Aは自所有の家屋（主物）をBに売却した。主物の効用を助ける従物（畳や建具等）は主物の処分に従うとする根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第87条2項 従物は、主物の処分に従う。" },
    { id: 15, cat: "第2回 民法総則", past: false, article: "第89条", title: "天然果実・法定果実", text: "〔設例〕果物等の「天然果実」や家賃等の「法定果実」の帰属を定める民法典の条数を【参考】条文から選択して答えよ。", content: "第89条1項 天然果率は分離時に帰属。 第89条2項 法定果率は存続期間に応じて日割計算。" },

    { id: 16, cat: "第3回 意思表示", past: true, article: "第97条", title: "到達主義", text: "〔設例〕AはBに対して契約解除の通知を発信した。意思表示はその通知が相手方に到達した時から効力を生ずる（到達主義）とする根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第97条1項 意思表示は、その通知が相手方に到達した時からその効力を生ずる。" },
    { id: 17, cat: "第3回 意思表示", past: true, article: "第93条", title: "心裡留保", text: "〔設例〕Aは冗談で「このダイヤモンドをただであげる」とBに言った。表意者が真意でないことを知りつつした意思表示の効力（相手方が悪意・有過失なら無効）を定める民法典の条数を【参考】条文から選択して答えよ。", content: "第93条1項 意思表示は、表意者が真意ではないことを知ってしたものであっても無効とならない。ただし相手方が悪意等の場合は無効。" },
    { id: 18, cat: "第3回 意思表示", past: true, article: "第94条", title: "虚偽表示", text: "〔設例〕AとBは通謀して「土地を売ったことにしよう」と嘘の売買契約を結んだ。相手方と通じてした虚偽の意思表示が無効となる根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第94条1項 相手方と通じてした虚偽の意思表示は、無効とする。" },
    { id: 19, cat: "第3回 意思表示", past: true, article: "第95条", title: "錯誤・動機錯誤", text: "〔設例〕Aは古伊万里だと思って骨とう品を購入したが贋作であった（動機錯誤）。基礎とした事情の認識が真実に反する錯誤の取り消しを規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第95条1項 意思表示は、重要部分に錯誤があるときは取り消すことができる。二 表意者が基礎とした事情の認識が真実に反する錯誤" },
    { id: 20, cat: "第3回 意思表示", past: true, article: "第96条", title: "詐欺・強迫", text: "〔設例〕Aは「家を買わないと危害を加える」と脅され（強迫）、恐怖で契約した。詐欺又は強迫による意思表示を取り消すことができる根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第96条1項 詐欺又は強迫による意思表示は、取り消すことができる。" },
    { id: 21, cat: "第3回 意思表示", past: true, article: "第119条", title: "無効行為の追認", text: "〔設例〕無効な法律行為は追認しても効力を生じないが、無効と知って追認したときは新たな法律行為とみなされる規定の民法典の条数を【参考】条文から選択して答えよ。", content: "第119条 無効な行為は追認しても効力を生じない。ただし無効と知って追認したときは新たな行為とみなす。" },
    { id: 22, cat: "第3回 意思表示", past: true, article: "第121条", title: "取消しの効果", text: "〔設例〕取り消された法律行為は初めから無効であったものとみなされる。この取消しの遡及効を定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第121条 取り消された行為は、初めから無効であったものとみなす。" },

    { id: 23, cat: "第4回 代理・時効", past: true, article: "第99条", title: "代理・顕名", text: "〔設例〕代理人Bは本人Aの権限内において「A代理人B」と名乗って（顕名）Cと契約した。効果が本人に直接帰属する根拠となる民法典の条数を【参考】条文から選択して答えよ。", content: "第99条1項 代理人がその権限内において本人のためにすることを示してした意思表示は、本人に対して直接にその効力を生ずる。" },
    { id: 24, cat: "第4回 代理・時効", past: false, article: "第108条", title: "自己契約・双方代理", text: "〔設例〕代理人Bが本人の代理人として自分自身と契約すること（自己契約）、または当事者双方の代理人となること（双方代理）の禁止を規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第108条1項 同一の法律行為については、相手方の代理人となり、又は当事者双方の代理人となることはできない。" },
    { id: 25, cat: "第4回 代理・時効", past: true, article: "第113条", title: "無権代理", text: "〔設例〕Bは代理権がないにもかかわらず勝手に「Aの代理人」として土地を売却した。本人が追認をしなければ効力を生じないとする民法典の条数を【参考】条文から選択して答えよ。", content: "第113条1項 代理権を有しない者が他人の代理人としてした契約は、本人がその追認をしなければ、本人に対してその効力を生じない。" },
    { id: 26, cat: "第4回 代理・時効", past: false, article: "第127条", title: "条件", text: "〔設例〕「大学に合格したらパソコンを買ってあげる」というように、条件成就により効力が発生する停止条件等を規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第127条1項 停止条件付法律行為は、停止条件が成就した時からその効力を生ずる。" },
    { id: 27, cat: "第4回 代理・時効", past: false, article: "第166条", title: "消滅時効", text: "〔設例〕債権は、権利を行使できることを知った時から5年間行使しないときは時効により消滅することを定める民法典の条数を【参考】条文から選択して答えよ。", content: "第166条1項1号 債権は、債権者が権利を行使することができることを知った時から五年間行使しないとき消滅する。" },

    { id: 28, cat: "第5回 債権・契約", past: true, article: "第533条", title: "同時履行の抗弁権", text: "〔設例〕売買契約において、相手方が債務の履行を提供するまでは自己の債務の履行を拒むことができる権利（同時履行の抗弁権）について定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第533条 双務契約の当事者の一方は、相手方がその債務の履行を提供するまでは、自己の債務の履行を拒むことができる。" },
    { id: 29, cat: "第5回 債権・契約", past: true, article: "第412条", title: "履行遅滞の時期", text: "〔設例〕確定期限がある債務において、債務者が期限到来時から遅滞の責任を負うこと（履行遅滞）を規定している民法典の条数を【参考】条文から選択して答えよ。", content: "第412条1項 債務の履行について確定期限があるときは、債務者は、その期限が到来した時から遅滞の責任を負う。" },
    { id: 30, cat: "第5回 債権・契約", past: true, article: "第412条の2", title: "履行不能", text: "〔設例〕売買契約の目的物が焼失し履行が不能となった場合について定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第412条の2第1項 債務の履行が社会通念上不能であるときは、債権者はその債務の履行を請求することができない。" },
    { id: 31, cat: "第5回 債権・契約", past: true, article: "第415条", title: "債務不履行による損害賠償", text: "〔設例〕債務者が本旨に従った履行をしないとき、債権者が損害賠償請求できる根拠となる民法典の条数を【参考】条文から選択して答えよ。", content: "第415条1項 債務者がその債務の本旨に従った履行をしないとき又は債務の履行が不能であるときは、債権者は損害賠償を請求できる。" },
    { id: 32, cat: "第5回 債権・契約", past: true, article: "第541条", title: "催告による解除", text: "〔設例〕債務不履行に対し相当期間を定めて催告をし、期間内に履行がない場合に契約解除できる根拠となる民法典の条数を【参考】条文から選択して答えよ。", content: "第541条 当事者の一方が債務を履行しない場合、相当の期間を定めて催告し期間内に履行がないときは契約の解除ができる。" },
    { id: 33, cat: "第5回 債権・契約", past: false, article: "第542条", title: "無催告解除", text: "〔設例〕債務の全部履行が不能である場合など、催告をすることなく直ちに契約解除できる場合を規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第542条1項1号 債務の全部の履行が不能であるときは、債権者は催告をすることなく直ちに契約の解除をすることができる。" },

    { id: 34, cat: "第6回 弁済等", past: true, article: "第473条", title: "弁済", text: "〔設例〕債務者が債権者に対して弁済をしたとき、その債権は消滅する旨を定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第473条 債務者が債権者に対して弁済をしたときは、その債権は消滅する。" },
    { id: 35, cat: "第6回 弁済等", past: false, article: "第484条", title: "弁済の場所", text: "〔設例〕弁済の場所の指定がない場合、特定物引渡しは債権発生時の存在場所で行う等の規定を定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第484条1項 別段の意思表示がないときは、特定物の引渡しは債権発生時に存在した場所、その他の弁済は債権者の現在住所で行う。" },
    { id: 36, cat: "第6回 弁済等", past: true, article: "第492条", title: "弁済の提供", text: "〔設例〕債務者は弁済の提供をした時から債務不履行責任を免れるという効果について定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第492条 債務者は、弁済の提供の時から、債務の不履行によって生ずべき責任を免れる。" },
    { id: 37, cat: "第6回 弁済等", past: false, article: "第505条", title: "相殺", text: "〔設例〕二人が互いに同種の債権を有する場合、対立する債権を対当額で消滅させる「相殺」について定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第505条1項 二人が互いに同種の目的を有する債権を有する場合、双方の債権が弁済期にあるときは相殺によって債務を免れることができる。" },
    { id: 38, cat: "第6回 弁済等", past: false, article: "第416条", title: "特別損害", text: "〔設例〕特別の事情によって生じた損害（特別損害）について予見可能性があった場合に賠償請求できる旨を定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第416条2項 特別の事情によって生じた損害であっても、当事者がその事情を予見し、又は予見することができたときは賠償を請求できる。" },
    { id: 39, cat: "第6回 弁済等", past: false, article: "第419条", title: "金銭債務の特則", text: "〔設例〕金銭債務の不履行における損害賠償額（法定利率）や不可抗力抗弁の不可等の特則を規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第419条1項 金銭の給付を目的とする債務の不履行については、損害賠償額は法定利率によって定める。" },

    { id: 40, cat: "第7回 契約不適合責任", past: true, article: "第562条", title: "追完請求権", text: "〔設例〕購入した新車に故障（契約不適合）があった場合、買主が修補や代替物引渡し等による「履行の追完」を請求できる根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第562条1項 目的物が契約内容に適合しないものであるときは、買主は売主に対し履行の追完（修補・代替物引渡し等）を請求できる。" },
    { id: 41, cat: "第7回 契約不適合責任", past: true, article: "第563条", title: "代金減額請求権", text: "〔設例〕追完催告をしたにもかかわらず追完がない場合、買主が不適合の程度に応じて「代金の減額」を請求できる根拠の民法典の条数を【参考】条文から選択して答えよ。", content: "第563条1項 相当の期間を定めて履行の追完の催告をし期間内に追完がないときは、買主は代金の減額を請求することができる。" },
    { id: 42, cat: "第7回 契約不適合責任", past: true, article: "第566条", title: "権利行使期間", text: "〔設例〕種類・品質の不適合を知った時から1年以内に売主に通知しなければ権利行使できなくなると定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第566条 売主が種類又は品質に関して契約内容に適合しない目的物を引き渡した場合、買主が知った時から一年以内に通知しないときは権利行使できない。" },
    { id: 43, cat: "第7回 契約不適合責任", past: true, article: "第545条", title: "原状回復義務", text: "〔設例〕契約解除時、各当事者が相手方を原状に復させる義務（原状回復義務）を負う旨を規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第545条1項 当事者の一方がその解除権を行使したときは、各当事者は、その相手方を原状に復させる義務を負う。" },

    { id: 44, cat: "第8回 典型契約", past: true, article: "第555条", title: "売買", text: "〔設例〕売主が財産権移転を約し、買主が代金支払いを約することで効力を生ずる「売買」について定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第555条 売買は、当事者の一方がある財産権を相手方に移転することを約し、相手方がこれに対してその代金を支払うことを約することによって効力を生ずる。" },
    { id: 45, cat: "第8回 典型契約", past: false, article: "第549条", title: "贈与", text: "〔設例〕当事者の一方が自己の財産を無償で与える意思を示し相手方が受諾して成立する「贈与」を定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第549条 贈与は、当事者の一方が自己の財産を無償で相手方に与える意思を表示し、相手方が受諾をすることによって効力を生ずる。" },
    { id: 46, cat: "第8回 典型契約", past: true, article: "第587条の2", title: "書面による消費貸借", text: "〔設例〕将来同額の金銭を返還することを約する消費貸借において、書面でする消費貸借の成立について定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第587条の2第1項 書面でする消費貸借は、当事者の一方が金銭等を引き渡すことを約し、相手方が同種のものを返還することを約することによって効力を生ずる。" },
    { id: 47, cat: "第8回 典型契約", past: false, article: "第601条", title: "賃貸借", text: "〔設例〕当事者の一方が物の使用・収益をさせ、相手方が賃料支払いおよび返還を約する「賃貸借」について定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第601条 賃貸借は、当事者の一方が相手方に物の使用及び収益をさせることを約し、相手方が賃料を支払うこと等を約することによって効力を生ずる。" },
    { id: 48, cat: "第8回 典型契約", past: true, article: "第632条", title: "請負", text: "〔設例〕Aが建築工事を依頼し、Bが仕事を完成させ、Aがその結果に対し報酬を支払う「請負」について定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第632条 請負は、当事者の一方がある仕事を完成することを約し、相手方がその仕事の結果に対してその報酬を支払うことを約することによって効力を生ずる。" },
    { id: 49, cat: "第8回 典型契約", past: false, article: "第644条", title: "善管注意義務", text: "〔設例〕委任契約において、受任者が負う「善良な管理者の注意義務（善管注意義務）」について規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第644条 受任者は、委任の本旨に従い、善良な管理者の注意をもって、委任事務を処理する義務を負う。" },

    { id: 50, cat: "第9回 約款等", past: true, article: "第548条の2", title: "定型約款", text: "〔設例〕鉄道の乗車券や保険契約など、画一的な取引の「定型約款」で個別条項が合意とみなされる要件を定めた民法典の条数を【参考】条文から選択して答えよ。", content: "第548条の2第1項 定型取引を行う合意をした者は、一定の場合に定型約款の個別の条項についても合意したものとみなす。" },
    { id: 51, cat: "第9回 約款等", past: false, article: "第548条の4", title: "定型約款の変更", text: "〔設例〕定型約款の変更が一般の利益に適合するとき等、事業者が一方的に約款変更できる旨を規定した民法典の条数を【参考】条文から選択して答えよ。", content: "第548条の4第1項 定型約款の準備者は、変更が相手方の一般の利益に適合するとき等に個別に合意することなく契約内容を変更できる。" },
    { id: 52, cat: "第9回 約款等", past: true, article: "消費者契約法", title: "消費者契約法", text: "〔設例〕事業者と消費者との契約について、民法の一般原則を修正して消費者を保護する法律名を答えよ。", content: "事業者と消費者との間の情報の質及び交渉力の格差にかんがみ、消費者の利益の擁護を図るための法律。" },

    { id: 53, cat: "第10回 電子商取引", past: true, article: "電子消費者契約法第3条", title: "電子消費者契約法3条", text: "〔設例〕ネット通販等で確認画面がない場合の消費者の操作ミス（クリックミス）による錯誤取消し（重過失適用の排除）を定めた条文を選択せよ。", content: "電子消費者契約法第3条 事業者が確認画面等の措置を講じていない場合、消費者の重過失による錯誤取消しの排除規定は適用されない。" },

    { id: 54, cat: "第11回 英米法", past: true, article: "約因（Consideration）", title: "英米法における契約成立要件", text: "〔設例〕英米法において契約の成立に必要とされる対価・交換取引の裏付けを示す概念（用語）として最も適切なものを選択せよ。", content: "英米法では契約成立のために意思の合致に加えて、交換取引の存在を裏付ける約因（Consideration）が必要とされる。" }
];

// --- アプリケーションの状態管理 ---
let currentMode = 1;
let currentQuestions = [];
let currentIndex = 0;
let userAnswers = {}; // { qIndex: { value, isCorrect } }
let bookmarks = {};   // { mode-id: boolean }
let isPastOnly = false;
const userNameStorageKey = "msLegalUserName";
const rankingStorageKey = "msLegalRanking";
let currentUserName = localStorage.getItem(userNameStorageKey) || "";
let leaderboard = loadRanking();

function setCurrentUserLabel() {
    const label = document.getElementById("current-user-label");
    if (!label) return;
    if (currentUserName) {
        label.innerText = `ログイン中: ${currentUserName}`;
        document.getElementById("user-name-input").value = currentUserName;
    } else {
        label.innerText = "";
    }
}

setCurrentUserLabel();

// --- アプリ初期化・画面切り替え ---

function switchModeSelect() {
    document.getElementById("mode-select-screen").classList.remove("hidden");
    document.getElementById("quiz-screen").classList.add("hidden");
    document.getElementById("result-screen").classList.add("hidden");
}

function selectMode(mode) {
    if (!currentUserName) {
        alert("ユーザー名を保存してください。ランキングに反映されます。");
        document.getElementById("user-name-input").focus();
        return;
    }

    currentMode = mode;
    isPastOnly = false;
    document.getElementById("past-only-btn").classList.remove("active");
    
    // データ初期化
    let sourceData = mode === 1 ? rawDataMode1 : rawDataMode2;
    currentQuestions = [...sourceData];
    
    currentIndex = 0;
    userAnswers = {};

    document.getElementById("mode-select-screen").classList.add("hidden");
    document.getElementById("quiz-screen").classList.remove("hidden");

    if (mode === 1) {
        document.getElementById("mode1-input").classList.remove("hidden");
        document.getElementById("mode2-options").classList.add("hidden");
    } else {
        document.getElementById("mode1-input").classList.add("hidden");
        document.getElementById("mode2-options").classList.remove("hidden");
    }

    renderQuestion();
}

// --- 問題ランダム＆絞り込み機能 ---

function shuffleQuestions() {
    for (let i = currentQuestions.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [currentQuestions[i], currentQuestions[j]] = [currentQuestions[j], currentQuestions[i]];
    }
    currentIndex = 0;
    userAnswers = {};
    renderQuestion();
}

function togglePastOnly() {
    isPastOnly = !isPastOnly;
    const btn = document.getElementById("past-only-btn");
    btn.classList.toggle("active", isPastOnly);

    let sourceData = currentMode === 1 ? rawDataMode1 : rawDataMode2;
    if (isPastOnly) {
        currentQuestions = sourceData.filter(q => q.past);
    } else {
        currentQuestions = [...sourceData];
    }
    currentIndex = 0;
    userAnswers = {};
    renderQuestion();
}

// --- 問題描画処理 ---

function renderQuestion() {
    if (currentQuestions.length === 0) {
        alert("該当する問題がありません。");
        return;
    }

    const q = currentQuestions[currentIndex];
    const bookmarkKey = `${currentMode}-${q.id}`;

    // UI更新
    document.getElementById("progress-text").innerText = `問題 ${currentIndex + 1} / ${currentQuestions.length}`;
    document.getElementById("question-title").innerText = `問 ${q.id}`;
    document.getElementById("question-text").innerText = q.text;
    document.getElementById("category-tag").innerText = q.cat;
    
    // 過去問タグ
    const pastTag = document.getElementById("past-tag");
    if (q.past) pastTag.classList.remove("hidden");
    else pastTag.classList.add("hidden");

    // ブックマークボタン
    const bmBtn = document.getElementById("bookmark-toggle");
    bmBtn.classList.toggle("active", !!bookmarks[bookmarkKey]);

    // フィードバックリセット
    const feedbackArea = document.getElementById("feedback-area");
    feedbackArea.classList.add("hidden");
    feedbackArea.className = "feedback hidden";

    if (currentMode === 1) {
        // 例1：記述モード
        const inputField = document.getElementById("type-answer");
        inputField.value = userAnswers[currentIndex]?.value || "";
        inputField.disabled = false;

        if (userAnswers[currentIndex]) {
            showFeedbackMode1(userAnswers[currentIndex].isCorrect);
        }
    } else {
        // 例2：シチュエーション選択モード
        renderMode2Options(q);
    }
}

// 例2 ダミー選択肢（他の問題の条文から3つ抽出）をランダム生成
function renderMode2Options(q) {
    const optionsContainer = document.getElementById("mode2-options");
    optionsContainer.innerHTML = "";

    // 正解以外の他の問題からランダムで3個の不正確選択肢を選ぶ
    const otherQuestions = rawDataMode2.filter(item => item.article !== q.article);
    const shuffledOthers = [...otherQuestions].sort(() => 0.5 - Math.random());
    const dummies = shuffledOthers.slice(0, 3);

    // 4つの選択肢を作成してシャッフル
    const choices = [q, ...dummies].sort(() => 0.5 - Math.random());

    choices.forEach(choice => {
        const btn = document.createElement("button");
        btn.className = "option-btn";
        
        // 選択肢テキスト（【参考】民法条文（抜粋）＋本文）
        btn.innerHTML = `<strong>【参考条文】${choice.article}</strong><br><small style="color:#555;">${choice.content}</small>`;
        
        btn.onclick = () => checkAnswerMode2(choice.article === q.article, q);
        
        if (userAnswers[currentIndex]) {
            btn.disabled = true;
            if (choice.article === q.article) {
                btn.style.borderColor = "var(--success-color)";
                btn.style.backgroundColor = "#e8f8f5";
            }
        }

        optionsContainer.appendChild(btn);
    });

    if (userAnswers[currentIndex]) {
        showFeedbackMode2(userAnswers[currentIndex].isCorrect, q);
    }
}

// --- 回答チェック処理 ---

function checkAnswerMode1() {
    if (userAnswers[currentIndex]) return; // 既に回答済み

    const q = currentQuestions[currentIndex];
    const userVal = document.getElementById("type-answer").value.trim();

    // 正誤判定（表記揺れ対応）
    const isCorrect = q.ans.some(ans => ans.toLowerCase() === userVal.toLowerCase());
    userAnswers[currentIndex] = { value: userVal, isCorrect: isCorrect };

    document.getElementById("type-answer").disabled = true;
    showFeedbackMode1(isCorrect);
}

function showFeedbackMode1(isCorrect) {
    const q = currentQuestions[currentIndex];
    const feedbackArea = document.getElementById("feedback-area");
    feedbackArea.classList.remove("hidden");

    if (isCorrect) {
        feedbackArea.className = "feedback correct";
        feedbackArea.innerHTML = `<strong>⭕ 正解！</strong>`;
    } else {
        feedbackArea.className = "feedback incorrect";
        feedbackArea.innerHTML = `<strong>❌ 不正解...</strong><br>正解: <strong>${q.ans[0]}</strong>`;
    }
}

function checkAnswerMode2(isCorrect, q) {
    if (userAnswers[currentIndex]) return; // 既に回答済み

    userAnswers[currentIndex] = { isCorrect: isCorrect };
    
    // 全選択肢を無効化
    const btns = document.querySelectorAll("#mode2-options .option-btn");
    btns.forEach(btn => btn.disabled = true);

    showFeedbackMode2(isCorrect, q);
}

function showFeedbackMode2(isCorrect, q) {
    const feedbackArea = document.getElementById("feedback-area");
    feedbackArea.classList.remove("hidden");

    if (isCorrect) {
        feedbackArea.className = "feedback correct";
        feedbackArea.innerHTML = `<strong>⭕ 正解！</strong><div class="article-box"><strong>正解条文: ${q.article}</strong><br>${q.content}</div>`;
    } else {
        feedbackArea.className = "feedback incorrect";
        feedbackArea.innerHTML = `<strong>❌ 不正解...</strong><div class="article-box"><strong>正解条文: ${q.article}</strong><br>${q.content}</div>`;
    }
}

// --- ブックマーク機能 ---

function toggleBookmark() {
    const q = currentQuestions[currentIndex];
    const key = `${currentMode}-${q.id}`;
    bookmarks[key] = !bookmarks[key];
    document.getElementById("bookmark-toggle").classList.toggle("active", bookmarks[key]);
}

// --- ナビゲーション ---

function prevQuestion() {
    if (currentIndex > 0) {
        currentIndex--;
        renderQuestion();
    }
}

function nextQuestion() {
    if (currentIndex < currentQuestions.length - 1) {
        currentIndex++;
        renderQuestion();
    }
}

// --- 採点＆結果機能 ---

function finishQuiz() {
    document.getElementById("quiz-screen").classList.add("hidden");
    document.getElementById("result-screen").classList.remove("hidden");

    let correctCount = 0;
    let answeredCount = Object.keys(userAnswers).length;

    Object.values(userAnswers).forEach(ans => {
        if (ans.isCorrect) correctCount++;
    });

    const total = currentQuestions.length;
    const percentage = Math.round((correctCount / total) * 100);

    document.getElementById("score-percentage").innerText = `${percentage}%`;
    document.getElementById("score-detail").innerText = `${total}問中 ${correctCount}問 正解 （回答済み: ${answeredCount}問）`;

    if (currentUserName) {
        updateLeaderboard(currentUserName, currentMode, correctCount);
        refreshRankingTable();
    }
}

function saveUserName() {
    const input = document.getElementById("user-name-input");
    const name = input.value.trim();
    if (!name) {
        alert("ユーザー名を入力してください。");
        input.focus();
        return;
    }
    currentUserName = name;
    localStorage.setItem(userNameStorageKey, currentUserName);
    setCurrentUserLabel();
    alert(`ユーザー名を保存しました: ${currentUserName}`);
}

function showRanking() {
    document.getElementById("mode-select-screen").classList.add("hidden");
    document.getElementById("quiz-screen").classList.add("hidden");
    document.getElementById("result-screen").classList.add("hidden");
    document.getElementById("ranking-section").classList.remove("hidden");
    refreshRankingTable();
}

function closeRanking() {
    document.getElementById("ranking-section").classList.add("hidden");
    document.getElementById("mode-select-screen").classList.remove("hidden");
}

function updateLeaderboard(name, mode, correctCount) {
    if (!name) return;

    const record = leaderboard.find(item => item.userName === name) || {
        userName: name,
        mode1Correct: 0,
        mode2Correct: 0
    };

    if (mode === 1) {
        record.mode1Correct = Math.max(record.mode1Correct, correctCount);
    } else {
        record.mode2Correct = Math.max(record.mode2Correct, correctCount);
    }

    if (!leaderboard.includes(record)) {
        leaderboard.push(record);
    }

    leaderboard.sort((a, b) => {
        const aTotal = (a.mode1Correct || 0) + (a.mode2Correct || 0);
        const bTotal = (b.mode1Correct || 0) + (b.mode2Correct || 0);
        if (bTotal !== aTotal) return bTotal - aTotal;
        return a.userName.localeCompare(b.userName, "ja");
    });

    localStorage.setItem(rankingStorageKey, JSON.stringify(leaderboard));
}

function loadRanking() {
    try {
        const rawValue = localStorage.getItem(rankingStorageKey);
        if (!rawValue) return [];
        return JSON.parse(rawValue);
    } catch (e) {
        console.error("ランキングの読み込みに失敗しました", e);
        return [];
    }
}

function refreshRankingTable() {
    const tbody = document.getElementById("ranking-table-body");
    tbody.innerHTML = "";
    if (!leaderboard || leaderboard.length === 0) {
        tbody.innerHTML = `<tr><td colspan="5">ランキングデータがありません。</td></tr>`;
        return;
    }

    leaderboard.forEach((item, index) => {
        const total = (item.mode1Correct || 0) + (item.mode2Correct || 0);
        tbody.insertAdjacentHTML("beforeend", `
            <tr>
                <td>${index + 1}</td>
                <td>${item.userName}</td>
                <td>${item.mode1Correct || 0}</td>
                <td>${item.mode2Correct || 0}</td>
                <td>${total}</td>
            </tr>
        `);
    });
}

function restartQuiz() {
    userAnswers = {};
    currentIndex = 0;
    document.getElementById("result-screen").classList.add("hidden");
    document.getElementById("quiz-screen").classList.remove("hidden");
    renderQuestion();
}

// 間違えた問題 ＋ 苦手チェック問題をまとめて復習
function retryMistakesOrBookmarks() {
    const reviewQuestions = currentQuestions.filter((q, index) => {
        const isWrong = userAnswers[index] && !userAnswers[index].isCorrect;
        const isBookmarked = !!bookmarks[`${currentMode}-${q.id}`];
        return isWrong || isBookmarked;
    });

    if (reviewQuestions.length === 0) {
        alert("復習する問題（間違い、または苦手チェックした問題）がありません！完璧です！");
        return;
    }

    currentQuestions = reviewQuestions;
    userAnswers = {};
    currentIndex = 0;

    document.getElementById("result-screen").classList.add("hidden");
    document.getElementById("quiz-screen").classList.remove("hidden");
    renderQuestion();
}
</script>
</body>
</html>
