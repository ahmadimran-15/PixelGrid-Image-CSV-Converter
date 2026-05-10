<h1 align="center">🎨 PixelGrid — Image ⇄ CSV Converter 🖼️</h1>

<p align="center">
  <em>Turn any image into a tidy table of pixels… tweak it… and turn it back into an image. ✨</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.7%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter">
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/Pillow-8A2BE2?style=for-the-badge&logo=python&logoColor=white" alt="Pillow">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=flat-square" alt="status">
  <img src="https://img.shields.io/badge/PRs-welcome-ff69b4?style=flat-square" alt="PRs">
  <img src="https://img.shields.io/badge/license-MIT-blue?style=flat-square" alt="license">
  <img src="https://img.shields.io/badge/made%20with-%E2%9D%A4-red?style=flat-square" alt="made with love">
</p>

---

## 🌟 Overview

**PixelGrid** is a small but cool computer-vision experiment built in a single Jupyter notebook. It does two things:

| 🔁 Direction | What it does |
|---|---|
| 🖼️ ➡️ 📊 **Image → CSV** | Reads an image, extracts **every pixel’s `(x, y)` position and `(R, G, B)` values**, plus the **R / G / B percentages** of `255`, and stores the whole thing as a clean `pandas` DataFrame and CSV. |
| 📊 ➡️ 🖼️ **CSV → Image** | Reads the (possibly edited) CSV, reshapes the pixel rows back into an `H × W × 4` array, and rebuilds the image as a brand new PNG. |

So you can literally **edit an image inside Excel / pandas** — change a column of red values, sort, filter, recolor a region — then regenerate the picture. 🪄

---

## 📑 Table of Contents

- [✨ Features](#-features)
- [🧠 How It Works](#-how-it-works)
- [📁 Project Structure](#-project-structure)
- [🛠️ Tech Stack](#%EF%B8%8F-tech-stack)
- [⚙️ Installation](#%EF%B8%8F-installation)
- [🚀 Usage](#-usage)
- [📊 CSV Schema](#-csv-schema)
- [🎨 Try It: Edit Pixels in CSV](#-try-it-edit-pixels-in-csv)
- [💡 Use Cases](#-use-cases)
- [🧰 Troubleshooting](#-troubleshooting)
- [🌱 Future Improvements](#-future-improvements)
- [📜 License](#-license)
- [👤 Author](#-author)

---

## ✨ Features

- 🎯 **Zero-loss pixel extraction** — every pixel and its coordinates are preserved.
- 📐 **Coordinates included** — `(x, y)` columns alongside `(R, G, B)` for spatial work.
- 💯 **RGB as percentages** — extra `R%`, `G%`, `B%` columns make the data instantly human-readable.
- 🧮 **Vectorized with NumPy** — fast reshaping using `np.indices` + `np.dstack`.
- 🐼 **Pandas-friendly output** — work with familiar DataFrames and `.csv` files.
- 🔄 **Round-trip rebuild** — convert back from CSV to a `PIL.Image` and save as PNG.
- 📓 **Single notebook** — everything is documented step-by-step in one place.

---

## 🧠 How It Works

```
   🖼️  image.png
        │
        ▼
   ┌──────────────────────────────────────────┐
   │  PIL.Image.open(...).convert("RGB")      │
   │  → numpy array (H, W, 3)                 │
   │  + np.indices  → (x, y) for every pixel  │
   │  → reshape to (N, 5) → DataFrame          │
   │  + R%, G%, B% columns                    │
   └──────────────────────────────────────────┘
        │
        ▼
   📊  rgb_percentage_xy_ValuesOfImage.csv
        │
        ▼  ✏️  edit values in Excel / pandas
        ▼
   📊  rgb_percentage_xy_ValuesOfImage_changed.csv
        │
        ▼
   ┌──────────────────────────────────────────┐
   │  read CSV → pick (red, green, blue)       │
   │  + Max_rgb_value=255 (alpha channel)      │
   │  → reshape to (W, H, 4) → uint8           │
   │  → Image.fromarray(...).save('new.png')   │
   └──────────────────────────────────────────┘
        │
        ▼
   🖼️  new.png
```

---

## 📁 Project Structure

```
PixelGrid-Image-CSV-Converter/
├── ImageToPix_PixToImage.ipynb              # 📓 The main Jupyter notebook
├── image.png                                # 🖼️ Source image (input)
├── new.png                                  # 🖼️ Reconstructed image (output)
├── xy_rgb_ValuesOfImage.csv                 # 📊 Pixels as (y, x, R, G, B)
├── rgb_percentage_xy_ValuesOfImage.csv      # 📊 Same + R% / G% / B% columns
├── rgb_percentage_xy_ValuesOfImage_changed.csv  # ✏️ Edited copy used for the rebuild
├── log.txt
├── .gitignore
└── README.md
```

---

## 🛠️ Tech Stack

| Tool | Role |
|---|---|
| 🐍 **Python 3.7+** | Language |
| 📓 **Jupyter Notebook** | Interactive workflow |
| 🖼️ **Pillow (PIL)** | Image read/write & RGB conversion |
| 🔢 **NumPy** | Pixel array math, reshaping, indices |
| 🐼 **pandas** | DataFrame & CSV I/O |

---

## ⚙️ Installation

### 1️⃣ Clone the repo

```bash
git clone https://github.com/ahmadimran-15/PixelGrid-Image-CSV-Converter.git
cd PixelGrid-Image-CSV-Converter
```

### 2️⃣ (Optional) Create a virtual environment

```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate
```

### 3️⃣ Install dependencies

```bash
pip install numpy pandas pillow notebook
```

---

## 🚀 Usage

### ▶️ Launch the notebook

```bash
jupyter notebook ImageToPix_PixToImage.ipynb
```

Then run the cells **top to bottom**. The notebook is split into two clear sections:

#### 🖼️ ➡️ 📊 Section 1 — Image to Pixels (CSV)

1. Place your input image as `image.png` in the project root (or change the filename in the first code cell).
2. Run the cells under **“Converting Image to Pixels In a CSV”**. They will:
   - Open the image with Pillow and convert it to RGB.
   - Build a NumPy array of every pixel’s position via `np.indices`.
   - Stack `(y, x, R, G, B)` into a single 2D array and wrap it in a DataFrame.
   - Save it as **`xy_rgb_ValuesOfImage.csv`**.
   - Add **`R%`**, **`G%`**, **`B%`** columns and save **`rgb_percentage_xy_ValuesOfImage.csv`**.

#### 📊 ➡️ 🖼️ Section 2 — Pixels (CSV) back to Image

1. Edit `rgb_percentage_xy_ValuesOfImage.csv` however you like (in Excel, pandas, a script…) and **save it as `rgb_percentage_xy_ValuesOfImage_changed.csv`**.
2. Run the cells under **“Converting Pixels From CSV to Image”**. They will:
   - Read your edited CSV.
   - Keep only the `red`, `green`, `blue` columns and append a constant alpha column (`Max_rgb_value = 255`).
   - Reshape to `(width, height, 4)`, cast to `uint8`, and rebuild a `PIL.Image`.
   - Save the result as **`new.png`**. 🎉

> 📝 **Note:** the rebuild step uses the `colourImg` object created in Section 1, so you must run Section 1 first (or hard-code the image dimensions in Section 2).

---

## 📊 CSV Schema

`rgb_percentage_xy_ValuesOfImage.csv` looks like this:

| index | y | x | red | green | blue | R% | G% | B% |
|------:|--:|--:|----:|------:|-----:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | 0.0 | 0.0 |
| 1 | 0 | 1 | 0 | 0 | 0 | 0.0 | 0.0 | 0.0 |
| … | … | … | … | … | … | … | … | … |

| Column | Type | Meaning |
|---|---|---|
| `y` | int | Row coordinate of the pixel. |
| `x` | int | Column coordinate of the pixel. |
| `red` / `green` / `blue` | int (0–255) | RGB channel values. |
| `R%` / `G%` / `B%` | float (0–100) | Channel value as a percentage of `255`. |

---

## 🎨 Try It: Edit Pixels in CSV

A few fun things to try once you have the CSV:

- 🔴 **Boost red everywhere** → set `red = 255` for all rows.
- 🌫️ **Grayscale** → set `red = green = blue = (red + green + blue) / 3`.
- 🟦 **Replace a color** → filter rows where `(red, green, blue)` matches a target color and overwrite them.
- 🪟 **Crop a region** → keep only rows where `x` and `y` fall in a chosen range, then resize the rebuild reshape accordingly.
- 🔁 **Mirror / flip** → swap `x` values via `x = (width - 1) - x` before saving.

Save the result as `rgb_percentage_xy_ValuesOfImage_changed.csv` and re-run Section 2 to see your edits. 🪄

---

## 💡 Use Cases

- 📚 **Teaching demo** — visualize what an image actually *is* (a grid of numbers).
- 🧪 **Image-processing experiments** without writing OpenCV/Numpy code from scratch.
- 🧰 **Data-science onboarding** — a friendly bridge between images, NumPy arrays, and DataFrames.
- 🎨 **Creative coding** — bulk recolor / remix images using spreadsheet logic.
- 🤖 **ML preprocessing prototype** — quickly inspect or massage pixel-level features.

---

## 🧰 Troubleshooting

| 🚧 Problem | 💡 Fix |
|---|---|
| `FileNotFoundError: image.png` | Put your input image in the project root or update the filename in cell 2. |
| `cannot reshape array of size N into shape (W,H,4)` | Make sure your edited CSV still has **exactly `width × height` rows** in the **same order** as when it was generated. |
| Output `new.png` looks rotated or stretched | The notebook reshapes as `(width, height, 4)` — if your image isn’t square, double-check `colourImg.size` and the reshape order. |
| Generated CSV is huge (tens of MB) | That is expected — even a small 800×600 image is 480,000 rows. Use Parquet or `to_csv(..., chunksize=...)` for very large images. |
| `ModuleNotFoundError: No module named 'PIL'` | Install Pillow: `pip install pillow`. |

---

## 🌱 Future Improvements

- 🧊 Use **Parquet / Feather** instead of CSV for massive speed & size wins.
- 🧱 Wrap the logic in a small **CLI** (`pixelgrid encode image.png` / `pixelgrid decode pixels.csv`).
- 🪄 Add **color-quantization** and **palette extraction** helpers.
- 🌐 Build a tiny **Streamlit / Flask** UI for upload → edit → download.
- 🧪 Add **unit tests** for the round-trip (image → CSV → image equality).
- 🅰️ Preserve a real **alpha channel** instead of forcing `255`.

---

## 📜 License

Released under the **MIT License** — free to use, modify, and share. ❤️

---

## 👤 Author

<p>
  <strong>Ahmad Imran</strong><br>
  🐙 GitHub: <a href="https://github.com/ahmadimran-15">@ahmadimran-15</a>
</p>

<p align="center">
  ⭐ <em>If this project sparked an idea, drop a star on the repo — it really helps!</em> ⭐
</p>
