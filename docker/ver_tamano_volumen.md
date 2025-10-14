# Ver tamaño de volumenes


```bash
docker volume ls -q \
| xargs -r -I {} sh -c '
  mp=$(docker volume inspect -f "{{ .Mountpoint }}" "{}" 2>/dev/null) || exit 0
  sz=$(sudo du -sb --apparent-size "$mp" 2>/dev/null | awk "{print \$1}")
  printf "%s\t%s\t%s\n" "${sz:-0}" "{}" "$mp"
' \
| sort -nr -k1,1 \
| awk -F'\t' 'BEGIN{printf "%10s  %-35s  %s\n","SIZE","VOLUME","MOUNTPOINT"}
  {cmd="numfmt --to=iec --suffix=B " $1; cmd | getline h; close(cmd);
   printf "%10s  %-35s  %s\n", h, $2, $3}'
```
