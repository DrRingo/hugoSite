+++
title = "Ringo's blog"
author = ["Ringo Stark"]
lastmod = 2024-04-13T21:39:19+07:00
draft = false
+++

## Posts {#posts}


### Các tác vụ thông thường về text {#các-tác-vụ-thông-thường-về-text}

Tất cả mọi thế giới của IT đều có thể quy về text, nên tác vụ text có vai trò lớn trong việc nâng cao năng suất.


#### Thay thế đoạn văn bản bị gãy dòng thành văn bản có dòng dài hơn, như tiêu chuẩn <span class="tag"><span class="shell">shell</span><span class="vim">vim</span></span> {#thay-thế-đoạn-văn-bản-bị-gãy-dòng-thành-văn-bản-có-dòng-dài-hơn-như-tiêu-chuẩn}

```search
SEARCH STRING: ((?:[^.?\n]$|\n(?!.?$)))\n
REPLACE STRING: $1
```

Lưu ý là có dấu cách " " ở cuối dòng replace string

EDITED: <span class="timestamp-wrapper"><span class="timestamp">[2023-06-08 Thu 20:43]</span></span>
Hoặc có thể viết theo lệnh `sed` như sau

<a id="code-snippet--enstring"></a>
```sh
sed 's/((?:[^.?\n]$|\n(?!.?$)))\n/$1 /g' FILENAME.ext
```


#### Căn chỉnh file timedot <span class="tag"><span class="emacs">emacs</span><span class="hledger">hledger</span></span> {#căn-chỉnh-file-timedot}

File timedot là một file hledger đặc biệt, nó gồm nhiều kí tự dot "." và cũng nhiều dòng chú thích theo sau. Vì vậy nó có thể căn chỉnh bằng lệnh align-regexp trong emacs để nhìn trật tự hơn. Và vì thế cũng giúp cho người ghi tự do hơn mà không sợ mất đi tính trật tự của file, miễn là vẫn đảm bảo được cấu trúc ngữ pháp.

```emacs
M-x align-regexp RET [[:space:]]\. RET
M-x align-regexp RET [;] RET
M-x align-regexp RET \([0-9]+h\) RET
```


#### Công thức thay thế ngày SCHEDULED bằng PROPERTIES <span class="tag"><span class="orgmode">orgmode</span><span class="regex">regex</span></span> {#công-thức-thay-thế-ngày-scheduled-bằng-properties}

Khi tôi viết orgmode trên android, rất khó để viết đầy đủ các thủ tục tiêu chuẩn orgmode, vì vậy tôi sử dụng chức năng SCHEDULED để tạo lập 1 ngày tháng viết cho nhanh, sau này trên máy tính sẽ sử dụng chức năng **'Find and Replace'** có _regex_ để thay thế toàn bộ 1 lần. Cụ thể như sau

```find_and_replace
FIND: SCHEDULED: <(\d*-\d*-\d* \w*)>
REPLACE: :PROPERTIES:\n:CREATED: [$1]\n:END:
```

EDITED:<span class="timestamp-wrapper"><span class="timestamp">[2023-02-10 Fri]</span></span>
Tôi đã tạo được một snippet đáng tin cậy trong vscode về việc ngày tháng, nên nếu tôi không ở trong vscode để tạo snippet thì tôi có thể viết đoạn snippet đó theo nguyên mẫu, để sau này tôi tạo lại chúng sau bằng vscode. Từ nay nên tránh dùng SCHEDULED vì sẽ dễ gây nhầm lẫn đâu là schedule thật, đâu là chỉ để thay thế thời gian tạo mục. Và cũng để tận dụng chức năng schedule tốt hơn.

EDITED: <span class="timestamp-wrapper"><span class="timestamp">[2023-05-11 Thu]</span></span>
Công thức vim hoặc emacs subtitute cho thay đổi ở trên, lợi thế là nó one-liner, chỉ cần copy và paste vô là hoạt động hiệu quả

```vim
%s/SCHEDULED: <\(.*\)>/:PROPERTIES:\n:CREATED: [\1]\n:END:/gc
```
