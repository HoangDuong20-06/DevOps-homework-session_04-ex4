# Bai 4: Quan ly file bo qua (.gitignore) va Sua lich su (Amend)

## 1. Boi canh
Vo tinh commit nham file chua thong tin bao mat `credentials.txt` len Git.
Can go bo file nay khoi su theo doi ma khong lam mat file vat ly tren dia cung,
cau hinh Git bo qua file nay trong tuong lai, va sua lai message commit gan nhat.

Rang buoc: khong dung lenh xoa vat ly (del/rm), phai giu lai tep tin o thu muc lam viec cuc bo.

## 2. Cach go bo file khoi cache: `git rm --cached`

```bat
git rm --cached credentials.txt
```

- `git rm` thong thuong: xoa file khoi index + xoa ca file vat ly tren dia.
- `git rm --cached`: chi xoa file khoi index (vung Staged/tracking), giu nguyen file vat ly.
- Sau lenh, `git status` hien:
  - `Changes to be committed: deleted: credentials.txt`
  - `Untracked files: credentials.txt`
- Kiem chung file van con: `dir credentials.txt` van thay file.

Day la lenh an toan dung cho file nhay cam da commit nham.

## 3. Cau hinh `.gitignore` de bo qua trong tuong lai

Them 1 dong vao `.gitignore`:
```
credentials.txt
```

Roi:
```bat
git add .gitignore
git check-ignore -v credentials.txt
git status
```

Ket qua thuc te:
```
.gitignore:38:credentials.txt  credentials.txt
```

`git status` sau do sach, `credentials.txt` khong con o Staged hay Modified.
`git ls-files | findstr credentials` tra ve rong = khong con track.

## 4. Sua commit gan nhat bang `--amend`

```bat
git commit --amend -m "Remove credentials, add gitignore"
```

- `--amend` viet lai commit cuoi (doi message va/hoac noi dung), sinh hash moi.
- Khong dung sau khi da push chung vi se lech lich su.
- O day dung de doi message tu "commit nham chua credentials"
  thanh "Remove credentials, add gitignore" dong thoi dua `.gitignore` vao cung commit.

## 5. Ket qua `git log -n 1` (chung minh amend thanh cong)

```
commit 3daa516355413729a647efc12c2703d8f0ef214a
Author: admin <hoangduong2062006@gmail.com>
Date:   Fri Oct 2 10:34:29 2026 +0700

    Remove credentials, add gitignore
```

Thong ke `--stat` khong con `credentials.txt` (11 files, toan code + gradle + gitignore).

## 6. Ket qua `git status`

```
On branch master
nothing to commit, working tree clean
```

Dat yeu cau: file `credentials.txt` van ton tai local (dir thay file),
nhung Git khong track, khong hien Staged/Modified.
