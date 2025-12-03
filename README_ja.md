# 蚊の電気生理学分析

[![Work In Progress](https://img.shields.io/badge/status-work%20in%20progress-yellow.svg)](https://github.com/groupmosquito/MosquitoSound)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

> **⚠️ 注意**: このリポジトリは進行中の研究およびプロジェクトです。プロジェクトの進展に伴い、コード、構造、方法論は大きく変更される可能性があります。

## 概要

このプロジェクトは、音響刺激に対する蚊の聴覚神経の電気生理学的記録を分析します。このパイプラインは、2種類の蚊（*Culex*および*Aedes aegypti*）の生の神経記録を、信号処理、特徴抽出、および分類と合成のためのディープラーニングモデルを通じて処理します。

### 研究目標
- 蚊の聴覚神経記録から神経応答パターンを抽出および分析
- ディープラーニングを使用して種特異的な聴覚応答を分類
- 敵対的生成ネットワーク（GAN）を使用して合成神経応答を生成
- 神経活性化を促進する主要な音響特徴を特定

## プロジェクトの状況

🚧 **開発中** - このリポジトリには実験的なコードと探索的な分析が含まれています。以下が予想されます：
- 頻繁な更新とリファクタリング
- データ処理パイプラインの変更
- モデルアーキテクチャの進化
- コードのクリーンアップとドキュメントの改善

**データに関する注意**: 生の電気生理学データは機密保持のため削除されています。ノートブックは方法論を示しており、同様のデータセットに適応できます。

## パイプラインアーキテクチャ

```
.smrファイル (Spike2) 
    ↓
WAV変換（バンドパスフィルタリング）
    ↓
特徴抽出（スペクトログラム/MFCC）
    ↓
ディープラーニングモデル（CNNオートエンコーダ、GAN）
    ↓
分析と合成
```

## ノートブック

### データ処理
- **`Sonogram_analysis.ipynb`** - Spike2ファイルからの初期データ探索とソノグラム生成
- **`wav_analysis.ipynb`** - .smrファイルをバンドパスフィルタリング（0-1000 Hz）でWAV形式に変換
- **`Converting to wav file.ipynb`** - 代替変換方法とGriffin-Lim再構成

### 特徴抽出とモデリング
- **`CNN_analysis.ipynb`** - スペクトログラム特徴抽出のための畳み込みオートエンコーダ
- **`CNN_recpmstruction.ipynb`** - オートエンコーダ再構成実験
- **`CNN_wav_analysis.ipynb`** - MFCCベースのCNN分類実験

### 生成モデル
- **`4_MFCCGAN_mrh020615.ipynb`** - MFCCからの音声合成のためのMelGANベースのアーキテクチャ

## 主要技術

- **信号処理**: Neo（Spike2ファイル読み取り）、SciPy（フィルタリング）、Librosa（音声特徴）
- **ディープラーニング**: TensorFlow/Keras（オートエンコーダ）、PyTorch（GAN）
- **データ分析**: NumPy、Pandas、Scikit-learn
- **可視化**: Matplotlib、Seaborn

## 技術仕様

### データ形式
- **ソース**: CED Spike2電気生理学記録（.smr）
- **サンプリングレート**: 100,000 Hz
- **種**: *Culex pipiens*および*Aedes aegypti*
- **前処理**: Butterworthバンドパスフィルタ（0-1000 Hz、次数4）

### モデルアーキテクチャ
- **CNNオートエンコーダ**: 128×128×3 RGBスペクトログラム → 潜在特徴
- **GAN**: 36個のMFCC係数を持つカスタムMelGAN変種
- **トレーニング**: `random_state=42`で80/20のトレーニング/テスト分割

## インストール

```bash
# リポジトリのクローン
git clone https://github.com/yourusername/MosquitoSound.git
cd MosquitoSound

# 仮想環境の作成
python -m venv venv
source venv/bin/activate  # Windowsの場合: venv\Scripts\activate

# 依存関係のインストール
pip install numpy pandas scipy scikit-learn
pip install librosa soundfile
pip install tensorflow torch torchvision
pip install neo matplotlib seaborn
pip install jupyter notebook
```

## 使用方法

**注意**: 生データは含まれていないため、これらのノートブックは方法論の例として機能します。独自のデータで使用するには：

1. Spike2 .smrファイルを`nerve_data_smr/{species}/`に配置
2. `wav_analysis.ipynb`を実行してWAV形式に変換
3. `CNN_analysis.ipynb`または`CNN_wav_analysis.ipynb`を使用してスペクトログラム/MFCCを生成
4. それぞれのノートブックを使用してモデルをトレーニング

## ディレクトリ構造

```
MosquitoSound/
├── notebooks/
│   ├── CNN_analysis.ipynb
│   ├── wav_analysis.ipynb
│   └── ...
├── models/              # 保存されたモデルチェックポイント（追跡されていません）
├── features/            # 抽出された特徴（追跡されていません）
├── MRH-Baseline/        # GANチェックポイント（追跡されていません）
```

## 今後の方向性

- [ ] 種間分類の実装
- [ ] 神経データ用GANアーキテクチャの最適化
- [ ] 包括的なユニットテストの追加
- [ ] インタラクティブな可視化ダッシュボードの作成
- [ ] 完全な実験プロトコルの文書化
- [ ] 事前トレーニング済みモデルの重みを追加（公開可能な場合）

## 貢献

これは開発中の研究プロジェクトです。フィードバック、提案、議論はIssuesを通じて歓迎します。

## 引用

このコードまたは方法論を研究で使用する場合は、以下を引用してください：

```
[出版時に引用情報を追加]
```

## ライセンス

MITライセンス - 詳細はLICENSEファイルを参照してください

## 連絡先

質問やコラボレーションについては、Issueを開くか、[あなたのメール]にお問い合わせください。

---

**免責事項**: このリポジトリには実験的な研究コードが含まれています。方法と結果は査読されておらず、本番環境または出版物で使用する前に検証する必要があります。
