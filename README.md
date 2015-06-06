# aozoraflow
Operation rules and tools to manage Aozora-bunko text files in a Git repository

## Aozoraflowとは

Aozoraflowは「青空文庫のテキストをGitリポジトリで管理する為の運用規約」と「それをサポートするためのツール」です。

## 運用規約

運用規約はちょうど[Vincent Driessenさんのブランチングモデル](http://nvie.com/posts/a-successful-git-branching-model/)で述べられているような、ブランチの作成・消去のルールです。実際、Aozoraflowはこのgit-flowブランチングモデルから大きな影響を受けています。さらにGitHubで広く知られることになったプルリクエストのモデルを組み合わせています。

### リポジトリの単位

作品毎にひとつのGitリポジトリを作ります。リポジトリ名は{作品ID}.gitになります。

### ブランチの種別

1. **edit**ブランチ

    編集中テキストが置かれるブランチ。実際の修正自体は後述のtypingブランチおよびproofingブランチで行われ、editブランチへはmergeされる事により変更が反映される。

1. **typing**ブランチ

    入力中のテキストが置かれるブランチ

1. **proofing**ブランチ

    校正中のテキストが置かれるブランチ

1. **master**ブランチ

    現在公開されている、あるいは過去に公開されたテキストが置かれるブランチ

### タグの種別

1. **TYPE_COMPLETE**

    全ての入力が完了したことを示すタグ

1. **PROOF_COMPLE**

    全ての校正が完了し、いつでも公開可能な状態であることを示すタグ

1. **PUBLISHED**

    現在公開中のバージョンを示すタグ

### 各作業の流れ

#### 入力作業

1. editブランチから枝分かれしてtypingブランチを作成する。
2. 入力途中でも変更を適宜typingブランチにコミットする。
3. 入力が完了したら、editブランチに対してマージするためのプルリクエストを出す。
4. リポジトリ管理者はプルリクエストを確認し、問題なければeditブランチにマージする。
5. 全ての入力が完了したら`TYPE_COMPLETE`のタグを付ける

<img src="https://docs.google.com/drawings/d/1AVIPo74Y3Aeyb61iAKKGJxNL-5mvdvkFeLFUPko2oiU/pub?w=953&amp;h=325">

#### 校正作業

1. editブランチから枝分かれしてproofingブランチを作成する。
2. 校正での修正を適宜proofingブランチに対してコミット。
3. 校正が完了したら、editブランチに対してマージするためのプルリクエストを出す
4. リポジトリ管理者はプルリクエストを確認し、問題なければeditブランチにマージする
5. 全ての校正が完了したら`PROOF_COMPLETE`のタグを付ける

#### 公開作業

1. 公開の基準を満たしていることを確認し、`PROOF_COMPLETE`のタグの付いたバージョンをmasterへマージする
2. マージしたコミットに`PUBLISHED`のタグを付ける


<img src="https://docs.google.com/drawings/d/1BaV1_SoalXpzB7FRW2apsHeC3RXutPM9yYdN47t6USA/pub?w=943&amp;h=743">
