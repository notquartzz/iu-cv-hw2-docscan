# ДЗ 2 «Сканер документов»

Инструмент `docscan.py` (Python 3, зависимости — `pip install -r requirements.txt`). Поиск листа через контуры или Хаф + RANSAC, перспективное выпрямление, удаление теней и бинаризация. Самопроверка: `python -m pytest tests -q`. Отчёт с числами и ответами — [REPORT.md](REPORT.md). Свои фотографии и разметка — в `data/`, результаты — в `out/`.

Основные команды (из корня репозитория):

```bash
python docscan.py annotate data/*.jpg --ann data/corners.json
python docscan.py noise data/01.jpg
python docscan.py noise data/10.jpg
python docscan.py noise data/13.jpg
python docscan.py noise data/01.jpg --add-sigma 5
python docscan.py noise data/01.jpg --add-sigma 10
python docscan.py noise data/01.jpg --add-sigma 25
python docscan.py edges data/01.jpg -o out/01_edges.png
python docscan.py edges data/01.jpg --close 0 -o out/01_edges_close0.png
python docscan.py edges data/07.jpg -o out/07_edges.png
python docscan.py edges data/07.jpg --close 0 -o out/07_edges_close0.png
python docscan.py eval data --ann data/corners.json --csv out/eval_default640.csv
python docscan.py eval data --ann data/corners.json --canny 50,150 --csv out/eval_fixed640.csv
python docscan.py eval data --ann data/corners.json --canny 50,150 --close 9 --long-side 1000 --seeds 20 --csv out/eval_1000_seeds20.csv
python docscan.py detect data/12.jpg --method auto --canny 50,150 --close 9 --long-side 1000 --ann data/corners.json -o out/12_detect.jpg
python docscan.py scan data/12.jpg --canny 50,150 --close 9 --long-side 1000 -o out/12_scan.jpg
python docscan.py binarize out/12_scan.jpg --method all -o out/12_binary.png
python docscan.py video --source 0 --method auto --canny 50,150 --close 9 --long-side 1000 --seconds 10 --save out/video.mp4
```

Выбранные параметры поиска: `--canny 50,150 --close 9 --long-side 1000`. Режим `auto` сначала пробует контуры, затем Хаф + RANSAC.

Полный список команд, сравнение настроек и команды для кадров курса (`sample_data/`) — в [REPORT.md](REPORT.md), раздел 5.
