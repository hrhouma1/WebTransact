
# 🤖 Méthode 4 : Automatisation via scripts Bash et Python

## Automatisation avec un script Bash :
```bash
#!/bin/bash
dir_v2="./accounts-v2"
dir_v3="./accounts-v3"
files_to_compare=("src/main/java/com/eazybytes/accounts/controller/AccountsController.java")

for file in "${files_to_compare[@]}"; do
    diff -u "$dir_v2/$file" "$dir_v3/$file" > "rapport_diff_${file}.txt"
    echo "Comparaison de $file terminée, différences enregistrées dans rapport_diff_${file}.txt"
done
```

## Automatisation avec un script Python :
```python
import os
import difflib

dir_v2 = './accounts-v2'
dir_v3 = './accounts-v3'

files_to_compare = ['src/main/java/com/eazybytes/accounts/controller/AccountsController.java']

def compare_files(file_v2, file_v3):
    with open(file_v2) as f1, open(file_v3) as f2:
        diff = difflib.unified_diff(f1.readlines(), f2.readlines(), fromfile=file_v2, tofile=file_v3)
        return ''.join(diff)

for file in files_to_compare:
    file_v2 = os.path.join(dir_v2, file)
    file_v3 = os.path.join(dir_v3, file)

    report = compare_files(file_v2, file_v3)
    report_file = f'rapport_diff_{file.replace("/", "_")}.txt'
    with open(report_file, 'w') as f:
        f.write(report)

    print(f'Comparaison de {file} terminée, rapport généré dans {report_file}.')
```

## Script Bash avancé :
```bash
#!/bin/bash
dir_v2="./accounts-v2"
dir_v3="./accounts-v3"
output_dir="./comparaison_rapports"
files_to_compare=("src/main/java/com/eazybytes/accounts/controller/AccountsController.java" "src/main/resources/application.properties")

mkdir -p $output_dir

for file in "${files_to_compare[@]}"; do
    diff -u --ignore-all-space "$dir_v2/$file" "$dir_v3/$file" > "$output_dir/rapport_diff_$(basename $file).txt"
    echo "Différences enregistrées dans $output_dir/rapport_diff_$(basename $file).txt"
done

echo "Résumé des différences :"
diff -rq "$dir_v2" "$dir_v3"
```
