# Kyoute2
import streamlit as st

st.set_page_config(page_title="共テ点数計算アプリ", layout="centered")  # 中央寄せでスマホ向け

st.title("共テ 各科目点数計算アプリ")

subjects = [
    "国語",
    "英語R",
    "英語L",
    "数学1A",
    "数学2B",
    "物理",
    "化学",
    "地理",
    "情報"
]

def digit_sum_or_raw(x):
    """
    x が 'g' で始まる → 'g' を除いた数値をそのまま返す（例：g55 → 55）
    それ以外 → 桁合計（例：55→10, 2222→8）
    """
    x = str(x).strip()

    if x.startswith("g"):
        raw = x[1:]
        if raw.isdigit():
            return int(raw)
        else:
            return 0

    if x.isdigit():
        return sum(int(d) for d in x)

    return 0

results = {}

st.header("点数入力（例：55 → 10、g55 → 55）")

# スマホ向けは縦並びで入力欄を広めに表示
for sub in subjects:
    score = st.text_input(f"{sub}:", value="0", max_chars=5)
    results[sub] = digit_sum_or_raw(score)

st.header("計算結果（各教科）")
for sub, val in results.items():
    st.write(f"{sub}: {val} 点")

# 合計点
total_score = sum(results.values())
st.header("合計点")
st.write(f"全教科合計: {total_score} 点")
