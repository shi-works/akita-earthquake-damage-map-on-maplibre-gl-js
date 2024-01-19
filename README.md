# MapLibre GL JSで秋田県地震被害想定マップ（震度分布図及び液状化危険度分布図）を表示するデモサイト
## デモサイト
https://shi-works.github.io/akita-earthquake-damage-map-on-maplibre-gl-js/

- 震度分布図及び液状化危険度分布図（PMTiles形式）
    - 出典：https://xs489works.xsrv.jp/pmtiles-data/pref-akita/akita-earthquake-data.pmtiles
        - 原初データ出典：[震度分布図及び液状化危険度分布図（シェープファイル）](https://www.pref.akita.lg.jp/pages/archive/53937)
        - ライセンス：[秋田県オープンデータ利用規約](https://www.pref.akita.lg.jp/pages/archive/36756)
    - 概要：秋田県のWebサイトにて公開されている、秋田県地震被害想定調査の震度分布図及び液状化危険度分布図（シェープファイル）をPMTiles形式に変換したデータです。
    - PMTiles形式のデータ作成方法
      - 作成時に対象としたデータは下記の8パターンです。
        - 01_能代断層帯
        - 02_花輪東断層帯
        - 03_男鹿地震
        - 04_天長地震
        - 05_秋田仙北地震震源北方
        - 06_北由利断層
        - 07_秋田仙北地震
        - 08_横手盆地東縁断層帯北部
      - 上記の8パターンのシェープファイルをPython（GDAL）でFlatGeobuf形式のデータに変換し、リネーム後、下記のtippecanoeのコマンドを実行して作成。
          - tippecanoeのコマンド
            ```
            tippecanoe -o akita-earthquake-data.pmtiles -Z8 -pf -pk -P \
            -L "{ \"id\": \"01\", \"file\": \"01.fgb\" }" \
            -L "{ \"id\": \"02\", \"file\": \"02.fgb\" }" \
            -L "{ \"id\": \"03\", \"file\": \"03.fgb\" }" \
            -L "{ \"id\": \"04\", \"file\": \"04.fgb\" }" \
            -L "{ \"id\": \"05\", \"file\": \"05.fgb\" }" \
            -L "{ \"id\": \"06\", \"file\": \"06.fgb\" }" \
            -L "{ \"id\": \"07\", \"file\": \"07.fgb\" }" \
            -L "{ \"id\": \"08\", \"file\": \"08.fgb\" }"
            ```
          - tippecanoeのバージョンはv2.23.0です。
      - PMTilesは、PMTiles Viewerで閲覧することができます。
      - https://protomaps.github.io/PMTiles/
