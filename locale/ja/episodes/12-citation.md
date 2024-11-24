---
title: 引用
teaching: 2
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- 自分の作品を引用しやすくする方法を学ぶ

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- 自分の作品をどのようにすれば引用しやすくできますか？

::::::::::::::::::::::::::::::::::::::::::::::::::

プロジェクトを参照する方法を記載した `CITATION` または `CITATION.txt` というファイルを含めると良いでしょう。  
Software Carpentry の場合、次のように記載されています：

```source
To reference Software Carpentry in publications, please cite:

Greg Wilson: "Software Carpentry: Lessons Learned". F1000Research,
2016, 3:62 (doi: 10.12688/f1000research.3-62.v2).

@online{wilson-software-carpentry-2016,
  author      = {Greg Wilson},
  title       = {Software Carpentry: Lessons Learned},
  version     = {2},
  date        = {2016-01-28},
  url         = {http://f1000research.com/articles/3-62/v2},
  doi         = {10.12688/f1000research.3-62.v2}
}
```

さらに詳しいアドバイスや、コードを引用可能にする他の方法については、  
[Software Sustainability Institute のブログ](https://www.software.ac.uk/publication/how-cite-and-describe-software) や以下の文献に記載されています：

```source
Smith AM, Katz DS, Niemeyer KE, FORCE11 Software Citation Working Group. (2016) Software citation
principles. [PeerJ Computer Science 2:e86](https://peerj.com/articles/cs-86/)
https://doi.org/10.7717/peerj-cs.8
```

また、対象のプロジェクトに引用すべき論文や書籍が存在しない場合は、[`@software{...`](https://www.google.com/search?q=git+citation+%22%40software%7B%22)
[BibTeX](https://www.ctan.org/pkg/bibtex) エントリタイプを使用することも可能です。

:::::::::::::::::::::::::::::::::::::::: keypoints

- リポジトリに CITATION ファイルを追加して、自分の作品をどのように引用してほしいかを説明する。

::::::::::::::::::::::::::::::::::::::::::::::::::
