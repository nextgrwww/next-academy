# 🎓 Next Academy

An interactive, self-contained educational platform designed to help students master GCSE and A-Level subjects through structured lessons, interactive quizzes, and gamified learning.

Built with **React**, **Tailwind CSS**, and **localStorage** persistence, it requires no build tools or dependencies—just open the file and start learning.

---

## ✨ Features

### Core Learning
- **Structured Courses** – Each course is divided into modules, with lessons that combine theory and quizzes.
- **Interactive Quiz Types** – Test your knowledge with multiple‑choice, fill‑in‑the‑blank, and drag‑to‑rearrange questions.
- **Markdown Rendering** – Theory slides support Markdown for clean formatting.
- **Progress Tracking** – Slide counters, module completion status, and overall course progress.
- **Practice Mode** – Direct access to module quizzes for targeted revision.

### Gamification & User Management
- **User Authentication** – Register and login with local storage (no server required).
- **Experience Points (XP)** – Earn XP by completing lessons and answering questions correctly.
- **Streak Tracking** – Build learning habits with consecutive daily activity tracking.
- **Leaderboard** – Compare your XP with other learners.
- **Course Certificates** – Receive a beautifully designed certificate when you complete a course.

### Personalisation
- **Dark / Light Mode** – Toggle themes with a single click (defaults to dark mode).
- **Profile Page** – View your progress, change password, and track course completion.
- **Tooltips & Popups** – Click on XP or Streak badges to learn how they work.

---

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/nextgrwww/next-academy.git
   cd next-academy
   ```

2. **Open `index.html`**  
   Just double‑click the file, or serve it with any static server (e.g., VS Code Live Server, Python's `http.server`, or Nginx).

3. **Create an account** – The authentication system uses `localStorage`, so no backend is required.

4. **Start learning** – Browse courses, work through lessons, and test your knowledge with quizzes.

---

## 📂 Project Structure

```
next-academy/
├── index.html          # Main application (all HTML, CSS, and JavaScript)
├── courses.json        # Course data (modules, lessons, theory, quizzes)
└── README.md           # This file
```

---

## 📚 Course Data Format

All course content is stored in `courses.json`. Each course has the following structure:

```json
{
  "id": "gcse-computer-science-j277",
  "level": "GCSE",
  "title": "Computer Science",
  "description": "An in-depth study of computer systems...",
  "color": "bg-blue-600",
  "textColor": "text-blue-600",
  "lightBg": "bg-blue-50",
  "iconName": "Cpu",
  "modules": [
    {
      "id": "cs_m1",
      "title": "Systems Architecture",
      "lessons": [
        {
          "id": "cs_m1_l1",
          "title": "The Purpose of the CPU and the Fetch-Execute Cycle",
          "isModuleQuiz": false,
          "steps": [
            {
              "type": "theory",
              "content": "**The Purpose of the CPU**\n\nThe Central Processing Unit..."
            },
            {
              "type": "quiz",
              "question": "What are the three stages of the fetch-execute cycle?",
              "options": ["Decode, Fetch, Execute", "Execute, Decode, Fetch", "Fetch, Decode, Execute", "Fetch, Execute, Decode"],
              "correctOption": 2,
              "explanation": "The correct order is always Fetch, then Decode, then Execute."
            },
            {
              "type": "fill_blank",
              "question": "The component that performs arithmetic and logical operations is called the ____.",
              "textBefore": "",
              "textAfter": "",
              "correctAnswer": "ALU",
              "explanation": "ALU stands for Arithmetic Logic Unit."
            },
            {
              "type": "rearrange",
              "question": "Arrange the FOIL steps in the correct order:",
              "items": ["First", "Outer", "Inner", "Last"],
              "correctOrder": ["First", "Outer", "Inner", "Last"],
              "explanation": "FOIL stands for First, Outer, Inner, Last."
            }
          ]
        },
        {
          "id": "cs_m1_quiz",
          "title": "Module 1 Review Quiz",
          "isModuleQuiz": true,
          "steps": [
            {
              "type": "quiz",
              "question": "Which component is responsible for performing arithmetic calculations?",
              "options": ["Control Unit", "Cache", "ALU", "MAR"],
              "correctOption": 2,
              "explanation": "The Arithmetic Logic Unit (ALU) handles all mathematical calculations."
            }
          ]
        }
      ]
    }
  ]
}
```

### Step Types
| Type | Description |
|------|-------------|
| `theory` | Educational content rendered with Markdown support. |
| `quiz` | Multiple‑choice question with options, correct answer index, and explanation. |
| `fill_blank` | Fill‑in‑the‑blank question with a `textBefore` and `textAfter` field. |
| `rearrange` | Drag‑and‑drop ordering task with `items` and `correctOrder`. |

### Lesson Properties
| Property | Type | Description |
|----------|------|-------------|
| `id` | `string` | Unique identifier for the lesson (used for progress tracking). |
| `title` | `string` | Display name of the lesson. |
| `isModuleQuiz` | `boolean` | If `true`, the lesson appears in the **Practice** tab. |
| `steps` | `array` | Array of step objects (theory, quiz, fill_blank, rearrange). |

---

## 🛠️ How It Works

### Architecture
- **React** manages UI state with hooks (`useState`, `useEffect`, `useRef`).
- **Tailwind CSS** provides utility‑first styling with dark mode support.
- **localStorage** persists user data, progress, and authentication.

### User Management
- Users are stored in `next_academy_users` (array of user objects).
- Active user is stored in `next_academy_active_user`.
- Each user has: `username`, `password`, `name`, `stats: { xp, streak, completedLessons }`.

### Progress Tracking
- Lesson completion is tracked per user via `completedLessons` array.
- Module completion requires all lessons in that module to be completed.
- Courses are locked until the previous module is finished.
- XP is awarded: `lesson.steps.length × 10` per completed lesson.

### Quiz Interaction
- **Multiple Choice** – Click an option, then click **CHECK** to validate.
- **Fill in the Blank** – Type your answer, then click **CHECK**.
- **Rearrange** – Drag and drop items (desktop drag‑and‑drop + mobile touch support), then click **CHECK**.

---

## 🔧 Customisation

### Add a New Course
1. Copy an existing course object in `courses.json`.
2. Update `id`, `title`, `description`, `color`, `textColor`, `lightBg`, and `iconName`.
3. Define modules and lessons with appropriate steps.

### Icon Mapping
The `iconName` field corresponds to icons defined in the `iconMap` object in `index.html`:

```javascript
const iconMap = {
    Calculator: <Calculator size={32} className="text-white" />,
    Code: <Code size={32} className="text-white" />,
    Atom: <Atom size={32} className="text-white" />,
    BookOpen: <BookOpen size={32} className="text-white" />,
    Trophy: <Trophy size={32} className="text-white" />
};
```

Add new icons by importing from [Lucide](https://lucide.dev/) or defining custom SVG components.

---

## 📜 Changelog

Based on recent commits:

### Mar 14, 2026
- ✅ Added slide counters, explanations, and SVG favicon
- ✅ Fixed long theory slides being cropped at the top
- ✅ Corrected indentation in `courses.json`
- ✅ Added more detail to GCSE Computer Science first chapter
- ✅ Added slide back button and Markdown rendering for theory content

### Mar 13, 2026
- ✅ Split chapters into multiple lessons in `courses.json`

### Mar 12, 2026
- ✅ Added slide back button and Markdown rendering
- ✅ Added first proper GCSE Computer Science course
- ✅ Fixed type mismatch crash on quiz slide transitions

### Mar 11, 2026
- ✅ Added support for multiple courses with external `courses.json`
- ✅ Dynamic fetching and merging of external courses
- ✅ Course completion detection with celebratory popup and SVG certificate
- ✅ Fixed Enter key on MCQ options
- ✅ Native touch drag-and-drop for rearrange quizzes
- ✅ Added practice mode, dynamic leaderboard, and profile progress filtering
- ✅ Implemented profile page, default dark mode, and auth screen theme toggle
- ✅ Fixed sign-in/register form input focus issue
- ✅ Added localStorage user authentication and progress tracking
- ✅ Added tooltips and instructional popups for XP and streak stats
- ✅ Initial `index.html` creation

---

## 🤝 Contributing

Contributions are welcome! If you have ideas for new courses, improvements to the UI, or bug fixes, please open an issue or submit a pull request.

### Development Notes
- The app is a single HTML file with inline React and Babel – no build step required.
- Test new courses by editing `courses.json` and refreshing the page.
- When adding new icons, update the `iconMap` object in `index.html`.

---

## 📄 License

This project is open‑source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgements

- **React** & **ReactDOM** – UI framework
- **Tailwind CSS** – Styling
- **Marked** – Markdown parsing
- **Lucide** – Icons
- **Babel Standalone** – JSX transpilation

---

*Happy learning!* 📖
