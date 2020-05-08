# notebook

1.从log文件中截取某段时间的log
sed -n  '/05-07 22:30:/,/05-07 22:37:/p' log_YAQBB20317200073.txt > 1.log
