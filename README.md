# MapLibre GL JSで秋田県地震被害想定マップ（震度分布図及び液状化危険度分布図）を表示するデモサイト
## デモサイト（下記の1～8のパターンを表示）
https://shi-works.github.io/akita-earthquake-damage-map-on-maplibre-gl-js/

## 震度分布図及び液状化危険度分布図（PMTiles形式）
- 出典（例：01.pmtilesが1. 能代断層帯です。）
1. [01.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/01.pmtiles)
2. [02.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/02.pmtiles)
3. [03.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/03.pmtiles)
4. [04.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/04.pmtiles)
5. [05.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/05.pmtiles)
6. [06.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/06.pmtiles)
7. [07.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/07.pmtiles)
8. [08.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/08.pmtiles)
9. [09.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/09.pmtiles)
10. [10.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/10.pmtiles)
11. [11.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/11.pmtiles)
12. [12.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/12.pmtiles)
13. [13.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/13.pmtiles)
14. [14.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/14.pmtiles)
15. [15.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/15.pmtiles)
16. [16.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/16.pmtiles)
17. [17.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/17.pmtiles)
18. [18.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/18.pmtiles)
19. [19.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/19.pmtiles)
20. [20.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/20.pmtiles)
21. [21.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/21.pmtiles)
22. [22.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/22.pmtiles)
23. [23.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/23.pmtiles)
24. [24.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/24.pmtiles)
25. [25.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/25.pmtiles)
26. [26.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/26.pmtiles)
27. [27.pmtiles](https://xs489works.xsrv.jp/pmtiles-data/pref-akita/27.pmtiles)

- 原初データ出典：[震度分布図及び液状化危険度分布図（シェープファイル）](https://www.pref.akita.lg.jp/pages/archive/7470)
- ライセンス：[秋田県オープンデータ利用規約](https://www.pref.akita.lg.jp/pages/archive/36756)
- 概要：秋田県のWebサイトにて公開されている、秋田県地震被害想定調査の震度分布図及び液状化危険度分布図（シェープファイル）をPMTiles形式に変換したデータです。

## PMTiles形式のデータ作成
- 作成時に対象としたデータは下記の[27パターン](https://www.pref.akita.lg.jp/pages/archive/53937)です。
1. 能代断層帯
2. 花輪東断層帯
3. 男鹿地震
4. 天長地震
5. 秋田仙北地震震源北方
6. 北由利断層
7. 秋田仙北地震
8. 横手盆地東縁断層帯北部
9. 横手盆地東縁断層帯南部
10. 真昼山地東縁断層帯北部
11. 真昼山地東縁断層帯南部
12. 象潟地震
13. 横手盆地_真昼山地連動
14. 秋田仙北地震震源北方_秋田仙北地震連動
15. 天長地震_北由利断層連動
16. 津軽山地西縁断層帯南部
17. 折爪断層
18. 雫石盆地西縁断層帯
19. 北上低地西縁断層帯
20. 庄内平野東縁断層帯
21. 新庄盆地断層帯
22. 海域A
23. 海域B
24. 海域C
25. 海域A＋B
26. 海域B＋C
27. 海域A＋B＋C

- 上記の27パターンのシェープファイルをPython（[GDAL/OGR](https://live.osgeo.org/ja/overview/gdal_overview.html)）でFlatGeobuf形式のデータに変換し、リネーム後、下記の[tippecanoe](https://github.com/felt/tippecanoe)のコマンドを実行して作成。
- tippecanoeのバージョンはv2.23.0です。
```sh:process_fgb_files.sh
#!/bin/bash

for input_file in *.fgb; do
    output_file="${input_file%.fgb}.pmtiles"
    echo "Processing ${input_file} ..."
    tippecanoe -o "${output_file}" "${input_file}" -Z8 -pf -pk -P 
done

echo "All files processed."
read -p "Press any key to continue . . . " -n1 -s
```

- PMTilesは、PMTiles Viewerで閲覧することができます（下記はPMTiles Viewerでパターン1を表示した例です）。
- ※url=部分のURLを書き換えると別のパターンでも表示ができます。
- https://protomaps.github.io/PMTiles/?url=https://xs489works.xsrv.jp/pmtiles-data/pref-akita/01.pmtiles#map=8.09/39.765/140.561
