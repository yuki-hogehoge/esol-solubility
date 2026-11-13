# ESOL 水溶解度データの探索的分析(RDKit)

RDKitで分子記述子を計算し、水溶解度(logS)との関係を調べる個人プロジェクトです。
「分子を眺めて仮説を立て、データで確かめ、条件をそろえて見直す」流れを、記録として残しています。

## 目的
- RDKitによる記述子計算と、データ分析の基本の型を復習する
- 相関と因果、交絡(条件をそろえる)を、化学の例で確かめる
- 記録を記事(Zenn)として公開する

## データ
- ESOL(Delaney)データセット(1,128分子、水溶解度の実測値)
- MoleculeNet / DeepChem で配布されているものを、ノートブック内で URL から読み込みます
- データ自体はこのリポジトリに含めていません(配布元のライセンスを確認してください)

## 進捗
| Day | 内容 | ノートブック | 記事 |
|---|---|---|---|
| 1 | データ確認、記述子の計算、相関と回帰(statsmodels) | `notebooks/01_eda_day1.ipynb` | `articles/esol-day1-eda.md` |
| 2 | ベースラインモデル(学習/検証分割、線形回帰、ランダムフォレスト) | (予定) | (予定) |

## Day 1 の主な結果
- logS と最も強く関連した記述子は LogP(相関 -0.83)
- 塩素(Cl)を含む分子は平均して溶けにくい(相関 -0.39)が、分子量の帯でそろえるとほぼ差が消える(重い分子の帯を除く)
- 回帰で LogP・分子量などを同時に入れると、nCl の係数はほぼ 0(+0.059)
- TPSA/MolWt より 1/MolWt のほうが logS と強く相関(0.54 対 0.46)。「極性の割合が大事」とは言い切れない

## 実行方法
Google Colab で `notebooks/01_eda_day1.ipynb` を開き、上から順に実行します。
ローカルの場合は `pip install -r requirements.txt` のあと、Jupyter で開いてください。

## 注意
- 相関は因果を意味しません。結果は ESOL データの範囲での観察です。
- RDKit の MolLogP は原子寄与の推定値で、実測値ではありません。

## 参考
- Delaney, J. S. (2004). ESOL: Estimating Aqueous Solubility Directly from Molecular Structure. J. Chem. Inf. Comput. Sci. ※書誌情報は公開前に確認
- Wu et al. (2018). MoleculeNet: a benchmark for molecular machine learning. Chem. Sci. ※同上
- RDKit: https://www.rdkit.org/
