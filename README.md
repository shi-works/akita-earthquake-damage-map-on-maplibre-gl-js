# MapLibre GL JSで秋田県地震被害想定マップ（震度分布図及び液状化危険度分布図）を表示するデモサイト
## デモサイト
https://shi-works.github.io/akita-earthquake-damage-map-on-maplibre-gl-js/

## 震度分布図及び液状化危険度分布図（PMTiles形式）
- 出典：https://xs489works.xsrv.jp/pmtiles-data/pref-akita/akita-earthquake-data.pmtiles
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
- tippecanoeのコマンド
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
- tippecanoeのバージョンはv2.23.0です。
- PMTilesは、PMTiles Viewerで閲覧することができます。
- https://protomaps.github.io/PMTiles/
