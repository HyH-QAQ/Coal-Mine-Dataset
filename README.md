## Feature Analysis of Overlapping Speech in Coal Mine Production Scheduling Scenarios



---

# 🚀 Uploading Like There's No Tomorrow

> ⚠️ **WARNING:** This project is still uploading. The author is currently battling slow Wi-Fi, existential dread, and mysterious bugs. Stay tuned. Don't rush.

---

## 🧠 What is this?

It’s a project that’s still halfway through uploading, but already aiming for the stars.
Could be code. Could be a model. Might even be a thesis draft wrapped in duct tape.
The files, the features, the occasional meltdown—all coming soon™.

## 🐢 Current Status

* [x] Renamed files at 3 AM
* [x] Uploaded the 999th `.pt` checkpoint manually
* [ ] Finished writing this README
* [ ] Upload complete (someday)
* [ ] Paper done (don’t ask)

## 🌪 Author's Condition

```bash
Status: Uploading...
ETA: Unknown
Stability: Questionable
Wi-Fi: Holding on for dear life
```

## 🧊 To Future Me (or You)

If you're reading this, it means the upload was successful.
Or I've collapsed somewhere, and my computer finished the job.
Either way—drop a ⭐️ to honor this heroic struggle against the void.

## 🎁 Easter Egg?

Maybe. When it’s all done. Maybe.

---

> **Uploading is hard. Reading is easy. Appreciate this moment.**
> — A human trying to sync their soul to GitHub

---
```mermaid
graph TD
    %% 节点样式定义（学术风配色）
    classDef raw fill:#e1f5fe,stroke:#01579b,stroke-width:2px,rx:5px,ry:5px;
    classDef process fill:#fff3e0,stroke:#e65100,stroke-width:2px,rx:5px,ry:5px;
    classDef model fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px,rx:5px,ry:5px;
    classDef dataset fill:#f3e5f5,stroke:#4a148c,stroke-width:2px,rx:5px,ry:5px;
    classDef final fill:#ede7f6,stroke:#311b92,stroke-width:3px,rx:10px,ry:10px,font-weight:bold;

    %% 1. 数据来源与预处理阶段
    RawData["原始音频数据采集<br/>(上榆泉矿调度室 145通录音)"]:::raw
    Pyannote["Pyannote 自动说话人分割<br/>(VAD与聚类)"]:::process
    Manual["人工专家甄别与筛选<br/>(剔除无效、归类对齐)"]:::process

    RawData ==> Pyannote
    Pyannote ==>|"提取包含单/双人的语音段"| Manual

    %% 2. 真实场景数据集分支
    subgraph "真实单人语音集 (Coal-single)"
        SingleNoisy["Coal-single-noisy<br/>(真实带噪单人语音)"]:::dataset
        DFCRN["DFCRN 语音增强模型<br/>(降噪处理)"]:::model
        SingleClean["Coal-single-DFCRN<br/>(降噪增强单人语音)"]:::dataset
    end

    subgraph "真实重叠语音集 (Coal-2mix)"
        RealMix["Coal-2mix 数据集<br/>(真实双人重叠语音)"]:::final
    end

    Manual -->|"提取双人重叠片段"| RealMix
    Manual -->|"提取单人片段"| SingleNoisy
    SingleNoisy -->|"输入带噪数据"| DFCRN
    DFCRN -->|"输出增强数据"| SingleClean

    %% 3. 合成混合数据集分支
    subgraph "合成混合语音集 (Coal-2mix-Synthesis)"
        MixProcess["wsj0-2mix 构建机制<br/>(按数据对进行合成)"]:::process
        Noisy2Mix["Coal-single-noisy-2mix<br/>(带噪合成混合)"]:::dataset
        Clean2Mix["Coal-single-DFCRN-2mix<br/>(纯净合成混合)"]:::dataset
        
        ExtractMix["提取 mix 文件夹<br/>(混合带噪特征)"]:::process
        ExtractS1S2["提取 s1, s2 文件夹<br/>(干净源目标特征)"]:::process
        
        FinalSynthesis["Coal-mixNoisy-singleClean<br/>(核心训练对数据集)"]:::final
    end

    SingleNoisy -.->|"提供合成数据对"| MixProcess
    SingleClean -.->|"提供合成数据对"| MixProcess
    
    MixProcess -->|"合成"| Noisy2Mix
    MixProcess -->|"合成"| Clean2Mix
    
    Noisy2Mix --> ExtractMix
    Clean2Mix --> ExtractS1S2
    
    ExtractMix ==>|"组合"| FinalSynthesis
    ExtractS1S2 ==>|"组合"| FinalSynthesis
```
