```python
isbn_number = [str(x) for x in input().strip()]
counter = 1

res = isbn_number[len(isbn_number)-1]
isbn_number = isbn_number[0:len(isbn_number)-1]

ans = 0
for character in isbn_number:
    if character == "-":
        continue
    ans = (ans + int(character) * counter % 11) % 11
    counter += 1

if ans == 10:
    ans = "X"
else:
    ans = str(ans)

if res == ans:
    print("Right")
else:
    print("".join(isbn_number), str(ans), sep="")