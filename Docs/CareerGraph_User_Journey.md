# CareerGraph User Journey

```
CareerGraph User Journey

Input Existing Career Data
          ↓
Build Professional Graph
          ↓
Analyze Target Vacancy
          ↓
Generate Positioning
          ↓
Prepare Application
          ↓
Track Outcome
          ↓
Update Graph
          ↓
Improve Future Matches
```

---

## 1. Graph — повний knowledge graph

Ми не спрощуємо до:

```
Skill → Project
```

А робимо:

```
                  Skill
                    |
                    |
Project ---- Evidence ---- Decision
    |             |
    |             |
Constraint ---- Impact
    |
    |
Experience
```

Це концептуальна модель. MVP не означає, що треба одразу робити Neo4j і малювати 3D граф. Можна почати на SQLite, просто правильно змоделювавши зв'язки.

---

## 2. Час — обов'язково

Без часу губиться кар'єра.

Не:

```
React
```

А:

```
React

2019
Learning

2021
Production project

2024
Architecture ownership

2026
Mentoring / decisions
```

Це дозволяє робити:

- skill evolution;
- career timeline;
- recommendations.

---

## 3. Source + Extracted Data

Варіант B.

Не:

```
CV.pdf
 ↓
Parser
 ↓
Delete PDF
```

А:

```
Original Source

CV.pdf
LinkedIn export
GitHub data
Notes

        ↓

Extraction Layer

        ↓

Professional Graph
```

Через рік AI стане кращим, парсер стане кращим — можна буде переобробити старі джерела.

---

## 4. Confidence

Не MVP, але залишаємо як поле на майбутнє.

Бо воно цікаве для AI.

```
Skill:
AWS

Evidence:
2 pet projects

Confidence:
Medium

Recommendation:
Need production evidence
```

Перша версія може жити без нього.

---

## 5. Wow pipeline

Один пайплайн, де кожен етап дає цінність.

---

### Stage 1 — "Я себе побачив"

Input:

- CV;
- LinkedIn;
- GitHub;
- ручні дані.

Output:

```
Your Professional Graph
```

Користувач бачить:

- скіли;
- проєкти;
- зв'язки;
- сильні сторони.

---

### Stage 2 — "Я зрозумів, чи підходжу"

Input:

Вакансія.

Output:

```
Match Analysis

84%

Strong:
React
TypeScript

Partial:
AWS

Missing:
Kubernetes
```

---

### Stage 3 — "Я краще себе продаю"

Generate:

- CV;
- cover letter;
- recruiter message;
- interview notes.

Але з графа.

---

### Stage 4 — "Я стаю кращим"

Після:

- rejection;
- interview;
- feedback.

Граф оновлюється.

```
Interview failed:

Reason:
System Design

↓

Career Insight:

Improve:
Architecture communication
```

---

Через 6 місяців CareerGraph вже не просто знає: "що ти вмієш". Він знає: "що тобі допомагає знаходити роботу". Це і є moat.