# 1. Selection Sort Algorithm : 선택 정렬 알고리즘
## 1) 정렬 알고리즘 이란?
- 정렬 알고리즘은 데이터를 일정한 조건에 맞게 정렬하는 알고리즘이다.
- 사용 빈도가 높고, 정렬할 데이터의 위치별 값의 비교횟수와 교환횟수에 따라서 성능이 달라진다.

## 2) 선택 정렬 알고리즘 이란?
- 선택 정렬 알고리즘은 첫 번째 데이터를 시작으로 끝부분까지 비교(compare)하면서 가장 작은 데이터가 나올 때까지 작은 데이터들과 자리를 바꾼다(swap).
- 그 다음은 두 번째 데이터를 시작으로 끝부분까지 훑어가면서 작은 데이터와 자리를 바꿈으로써 전체 데이터를 정렬 시킨다.
	```
	* 가장 작은 데이터를 선택하여 가장 왼쪽 아이템과 교환하는 방식
	```
## 보충 설명
    - 첫 번째 데이터 바로 앞의 데이터와 비교하면서 마지막 데이터까지 작업을 수행한다. 한 칸 앞의 데이터와 비교한 후, 작은 데이터가 나오면 그 작은 데이터를 min 값에 저장한 후 다음 앞의 데이터와 비교한다. 즉 현재 min 데이터보다 더 작은 데이터를 만나면 더 작은 데이터를 min 에 저장한 후 이 더 작은 min 데이터를 마지막 데이터까지 비교한다. 
    - 이 더 작은 min 데이터가 끝까지 비교해도 여전히 작다면, 이 min 데이터는 전체 배열중에서 가장 작은 데이터이므로 첫 번쨰 데이터와 자리를 교환한다. 
    - 만약 최초의 첫번째 데이터가 가장 작은 데이터 였다면, min 변수의 데이터 변경이 없이 마지막 데이터까지 비교하게 된다.
    - 즉 1번째 데이터를 뒤의 데이터와 비교하면서 더 작은 것이 나오면 이 것을 그 뒤의 데이터와 비교하는 방식이므로 1회전을 할 때 전체 배열에서 가장 작은 데이터가 결정되는 방식이다.
    - 비교하는 도중에 자리 교환이 일어나지 않고 한 회전이 끝날 때 비교를 시작한 데이터와 자리를 교환한다. 
    - 비교 대상이 현재 데이터보다 뒤에 있다.
    - 
## 3) 선택 정렬 알고리즘 코드

- 데이터 생성
- 정렬할 데이터의 수를 입력받은 후, 랜덤으로 숫자를 생성하고 리스트에 저장한다.
```
import random
import time
import copy

if __name__ == '__main__' :
    list = []

    input_n = input("정렬할 데이터의 수 : ")
    for i in range(int(input_n)) :
        list.append(random.randint(1, int(input_n)))

    list_copy = copy.copy(list)    # 다른 알고리즘에서도 같은 리스트를 사용하기 위한 얕은복사
```

- 코드
- 500 개의 데이터 생성
```
compare_counter = 0 # 비교 횟수
swap_counter = 0    # 교환 횟수

def selection_sort(random_list) :
    global compare_counter, swap_counter

    for sel in range(len(random_list)-1) :
        min = random_list[sel]     # 현재 데이터를 min 에 저장
        minindex = sel             # 현재 데이터의 인덱스를 minindex 에 저장

        # find min value
        for step in range(sel+1, len(random_list)) :     # 상위 for 문 보다 한 칸 앞에서부터 시작하는 하위 for 문
            compare_counter += 1
            if min > random_list[step] :                 # min 에 저장된 값과 한 칸 앞의 데이터 값을 비교. 현재 값이 더 크면
                min = random_list[step]                  # min 에 현재 값이 아닌 더 작은 값을 저장. step 이 sel 보다 한 칸 앞
                minindex = step                          # minindex 를 step 으로 저장. 다시 for 문에서 min 과 그 다음 데이터를 비교

        # swap
        swap_counter += 1
        random_list[minindex] = random_list[sel]         # min 에 저장된 값이 한 칸 앞의 데이터 값보다 작으면, 위치를 바꿀 필요가 없음.
        random_list[sel] = min                           # 따라서 현재 데이터를 현재 위치에 그대로 둠.
```

- 출력
```
print("정렬하기 전 :")
print(list)
print("\n")
start_time = time.time()
selection_sort(list)
running_time = time.time() - start_time

print("정렬한 후 : ")
print(list)
print("\n")

print("데이터의 크기 : {}".format(int(input_n)))
print("정렬 시간 : {}".format(running_time))
print("비교 횟수 : {}".format(compare_counter))
print("교환 횟수 : {}".format(swap_counter))
=================================================
정렬하기 전 :
[258, 451, 431, 426, 392, 371, 60, 154, 111, 61, 494, 68, 371, 482, 484, 24, 468, 235, 264, 343, 17, 11, 499, 33, 371, 236, 416, 348, 319, 329, 356, 201, 263, 479, 163, 422, 223, 140, 445, 43, 483, 459, 449, 360, 51, 418, 173, 416, 437, 147, 261, 437, 14, 42, 471, 50, 208, 179, 167, 287, 202, 301, 10, 119, 391, 443, 30, 477, 128, 442, 114, 228, 473, 173, 66, 122, 146, 248, 370, 212, 412, 275, 2, 28, 447, 288, 271, 55, 128, 12, 210, 221, 126, 282, 292, 270, 447, 293, 129, 321, 461, 237, 478, 226, 228, 358, 164, 149, 167, 15, 53, 191, 189, 249, 316, 134, 318, 355, 217, 467, 206, 203, 319, 338, 343, 8, 476, 301, 121, 125, 270, 273, 486, 126, 228, 494, 121, 377, 175, 144, 183, 244, 431, 117, 285, 498, 367, 294, 335, 198, 354, 159, 363, 301, 410, 30, 313, 152, 149, 354, 421, 452, 450, 444, 138, 499, 116, 28, 265, 339, 477, 138, 109, 264, 256, 399, 421, 466, 196, 385, 68, 466, 165, 351, 79, 220, 80, 277, 289, 289, 406, 226, 189, 464, 200, 430, 61, 366, 150, 239, 419, 71, 144, 422, 320, 227, 83, 259, 156, 399, 376, 240, 59, 4, 21, 88, 188, 437, 413, 193, 93, 370, 349, 181, 442, 33, 466, 333, 471, 438, 120, 41, 404, 362, 366, 64, 255, 208, 298, 135, 275, 325, 356, 346, 33, 198, 100, 22, 56, 374, 248, 141, 181, 18, 268, 207, 211, 84, 84, 427, 180, 256, 295, 438, 500, 456, 271, 221, 177, 440, 301, 16, 69, 305, 98, 2, 246, 414, 125, 312, 46, 267, 499, 219, 47, 41, 152, 321, 135, 406, 244, 349, 433, 90, 407, 189, 389, 208, 76, 464, 46, 39, 138, 230, 334, 88, 448, 387, 12, 387, 240, 309, 138, 105, 18, 161, 335, 138, 94, 265, 169, 150, 225, 479, 455, 490, 204, 415, 202, 381, 129, 155, 342, 125, 459, 195, 152, 284, 115, 7, 350, 244, 217, 259, 295, 344, 475, 139, 456, 190, 390, 18, 226, 489, 204, 233, 346, 423, 323, 367, 139, 263, 111, 235, 27, 374, 442, 155, 254, 182, 188, 330, 490, 499, 208, 424, 420, 3, 313, 498, 444, 297, 135, 298, 274, 271, 256, 53, 153, 368, 411, 331, 143, 241, 146, 429, 443, 76, 252, 364, 336, 313, 178, 28, 207, 2, 36, 289, 135, 339, 268, 485, 106, 376, 378, 281, 184, 145, 429, 44, 408, 61, 382, 411, 7, 396, 399, 155, 382, 161, 370, 149, 254, 445, 457, 109, 419, 21, 343, 122, 29, 406, 89, 296, 122, 176, 305, 199, 181, 329, 136, 298, 134, 168, 201, 484, 249, 94, 291, 42, 188, 448, 325, 409, 76, 52, 280, 471, 244, 311, 468, 170, 260, 385, 85, 40, 271, 265, 462, 495, 433, 1, 159, 380, 457, 264, 259, 491, 346, 167, 278, 41, 188, 160, 476, 438, 481, 180, 279, 46]


정렬한 후 :
[1, 2, 2, 2, 3, 4, 7, 7, 8, 10, 11, 12, 12, 14, 15, 16, 17, 18, 18, 18, 21, 21, 22, 24, 27, 28, 28, 28, 29, 30, 30, 33, 33, 33, 36, 39, 40, 41, 41, 41, 42, 42, 43, 44, 46, 46, 46, 47, 50, 51, 52, 53, 53, 55, 56, 59, 60, 61, 61, 61, 64, 66, 68, 68, 69, 71, 76, 76, 76, 79, 80, 83, 84, 84, 85, 88, 88, 89, 90, 93, 94, 94, 98, 100, 105, 106, 109, 109, 111, 111, 114, 115, 116, 117, 119, 120, 121, 121, 122, 122, 122, 125, 125, 125, 126, 126, 128, 128, 129, 129, 134, 134, 135, 135, 135, 135, 136, 138, 138, 138, 138, 138, 139, 139, 140, 141, 143, 144, 144, 145, 146, 146, 147, 149, 149, 149, 150, 150, 152, 152, 152, 153, 154, 155, 155, 155, 156, 159, 159, 160, 161, 161, 163, 164, 165, 167, 167, 167, 168, 169, 170, 173, 173, 175, 176, 177, 178, 179, 180, 180, 181, 181, 181, 182, 183, 184, 188, 188, 188, 188, 189, 189, 189, 190, 191, 193, 195, 196, 198, 198, 199, 200, 201, 201, 202, 202, 203, 204, 204, 206, 207, 207, 208, 208, 208, 208, 210, 211, 212, 217, 217, 219, 220, 221, 221, 223, 225, 226, 226, 226, 227, 228, 228, 228, 230, 233, 235, 235, 236, 237, 239, 240, 240, 241, 244, 244, 244, 244, 246, 248, 248, 249, 249, 252, 254, 254, 255, 256, 256, 256, 258, 259, 259, 259, 260, 261, 263, 263, 264, 264, 264, 265, 265, 265, 267, 268, 268, 270, 270, 271, 271, 271, 271, 273, 274, 275, 275, 277, 278, 279, 280, 281, 282, 284, 285, 287, 288, 289, 289, 289, 291, 292, 293, 294, 295, 295, 296, 297, 298, 298, 298, 301, 301, 301, 301, 305, 305, 309, 311, 312, 313, 313, 313, 316, 318, 319, 319, 320, 321, 321, 323, 325, 325, 329, 329, 330, 331, 333, 334, 335, 335, 336, 338, 339, 339, 342, 343, 343, 343, 344, 346, 346, 346, 348, 349, 349, 350, 351, 354, 354, 355, 356, 356, 358, 360, 362, 363, 364, 366, 366, 367, 367, 368, 370, 370, 370, 371, 371, 371, 374, 374, 376, 376, 377, 378, 380, 381, 382, 382, 385, 385, 387, 387, 389, 390, 391, 392, 396, 399, 399, 399, 404, 406, 406, 406, 407, 408, 409, 410, 411, 411, 412, 413, 414, 415, 416, 416, 418, 419, 419, 420, 421, 421, 422, 422, 423, 424, 426, 427, 429, 429, 430, 431, 431, 433, 433, 437, 437, 437, 438, 438, 438, 440, 442, 442, 442, 443, 443, 444, 444, 445, 445, 447, 447, 448, 448, 449, 450, 451, 452, 455, 456, 456, 457, 457, 459, 459, 461, 462, 464, 464, 466, 466, 466, 467, 468, 468, 471, 471, 471, 473, 475, 476, 476, 477, 477, 478, 479, 479, 481, 482, 483, 484, 484, 485, 486, 489, 490, 490, 491, 494, 494, 495, 498, 498, 499, 499, 499, 499, 500]


데이터의 크기 : 500
정렬 시간 : 0.04987001419067383
비교 횟수 : 124750
교환 횟수 : 499
```

# 2. Insert Sort Algorithm : 삽입 정렬 알고리즘
## 1) 삽입 정렬 알고리즘이란 ?
- 선택 정렬 알고리즘과 유사하지만 전체 데이터에서 작은 값을 검색하는 과정 없이, 순차적으로 정렬한다.
- 현재의 값과 이미 정렬이 끝난 값들을 비교하여 해당 위치로 삽입하는 방식이다.
	```
	* 정렬되지 않은 데이터에서 순서대로 데이터를 뽑아서 정렬된 데이터의 들어갈 위치를 찾아 삽입하는 방식
 	```
## 보충 설명 
- 삽입 정렬 알고리즘은 뒤에 있는 데이터를 그 앞에 있는 데이터들과 비교하고, 작은 것이 있으면 교환하는 방식이다.
- 따라서 뒤의 데이터 일 수록 앞의 데이터는 이미 정렬이 되어 있으므로, 바로 앞의 데이터와 비교해서 작지 않다면 더이상 비교 작업을 수행하지 않는다.
- 4번째 데이터를 비교할 차례에서는 이미 1,2,3 번째는 정렬이 된 상태이다. 4번째와 3번째 비교후 작은 것을 2번째와 비교하고, 여기에서 작은 데이터를 첫번째데이터와 비교한다. 즉 4번째 데이터가 3번째보다 작다면 이 데이터가 첫번째 데이터까지 비교한 후 자리를 교환하게 된다. 4번째 데이터가 3번째 데이터보다 크다면 교환 없이 5번째 데이터의 비교가 시작된다.
- 비교대상이 현재 데이터보다 앞에 있다.

## 2) 삽입 정렬 알고리즘 코드
- 코드
```
compare_counter_2 = 0
swap_counter_2 = 0

def insertion_sort(my_list) :
    global compare_counter_2, swap_counter_2
    my_list.insert(0, -1)     # 데이터의 첫 번째 값을 -1 로 저장

    for s_idx in range(2, len(my_list)) :     # 리스트의 2번째 데이터부터 끝까지.
        temp = my_list[s_idx]                 # 현재 2번째 데이터의 값을 temp 에 저장
        ins_idx = s_idx                       # 현재 데이터의 인덱스를 ins_idx 에 저장
        compare_counter_2 += 1                # 비교 횟수 저장

        while my_list[ins_idx - 1] > temp :              # 현재 데이터와 한칸 뒤에 있는 데이터와 비교. 정렬 된 데이터 사이로 작은 값 삽입.
            swap_counter_2 += 1                          # 교환 횟수 저장
            my_list[ins_idx] = my_list[ins_idx - 1]      # 한칸 뒤에 있는 데이터가 현재 데이터보다 크면, 현재 위치의 값을 작은 값으로 교환.
            ins_idx = ins_idx - 1                        # 현재 인덱스를 한칸 뒤의 인덱스로 저장 후 while 문 반복.

        my_list[ins_idx] = temp               # 현재 데이터 값보다 한칸 뒤의 데이터 값이 더 작으면, 현재 값 그대로 저장.
    del my_list[0]
```
- 출력
```
print("정렬하기 전 : ")
print(list_copy)
print("\n")

start_time_2 = time.time()
insertion_sort(list_copy)
running_time_2 = time.time() - start_time_2

print("정렬한 후 : ")
print(list_copy)
print("\n")

print("데이터의 수 : {}".format(int(input_n_2)))
print("정렬 시간 : {}".format(running_time_2))
print("비교 횟수 : {}".format(compare_counter_2))
print("교환 횟수 : {}".format(swap_counter_2))
========================================================
정렬하기 전 : 
[258, 451, 431, 426, 392, 371, 60, 154, 111, 61, 494, 68, 371, 482, 484, 24, 468, 235, 264, 343, 17, 11, 499, 33, 371, 236, 416, 348, 319, 329, 356, 201, 263, 479, 163, 422, 223, 140, 445, 43, 483, 459, 449, 360, 51, 418, 173, 416, 437, 147, 261, 437, 14, 42, 471, 50, 208, 179, 167, 287, 202, 301, 10, 119, 391, 443, 30, 477, 128, 442, 114, 228, 473, 173, 66, 122, 146, 248, 370, 212, 412, 275, 2, 28, 447, 288, 271, 55, 128, 12, 210, 221, 126, 282, 292, 270, 447, 293, 129, 321, 461, 237, 478, 226, 228, 358, 164, 149, 167, 15, 53, 191, 189, 249, 316, 134, 318, 355, 217, 467, 206, 203, 319, 338, 343, 8, 476, 301, 121, 125, 270, 273, 486, 126, 228, 494, 121, 377, 175, 144, 183, 244, 431, 117, 285, 498, 367, 294, 335, 198, 354, 159, 363, 301, 410, 30, 313, 152, 149, 354, 421, 452, 450, 444, 138, 499, 116, 28, 265, 339, 477, 138, 109, 264, 256, 399, 421, 466, 196, 385, 68, 466, 165, 351, 79, 220, 80, 277, 289, 289, 406, 226, 189, 464, 200, 430, 61, 366, 150, 239, 419, 71, 144, 422, 320, 227, 83, 259, 156, 399, 376, 240, 59, 4, 21, 88, 188, 437, 413, 193, 93, 370, 349, 181, 442, 33, 466, 333, 471, 438, 120, 41, 404, 362, 366, 64, 255, 208, 298, 135, 275, 325, 356, 346, 33, 198, 100, 22, 56, 374, 248, 141, 181, 18, 268, 207, 211, 84, 84, 427, 180, 256, 295, 438, 500, 456, 271, 221, 177, 440, 301, 16, 69, 305, 98, 2, 246, 414, 125, 312, 46, 267, 499, 219, 47, 41, 152, 321, 135, 406, 244, 349, 433, 90, 407, 189, 389, 208, 76, 464, 46, 39, 138, 230, 334, 88, 448, 387, 12, 387, 240, 309, 138, 105, 18, 161, 335, 138, 94, 265, 169, 150, 225, 479, 455, 490, 204, 415, 202, 381, 129, 155, 342, 125, 459, 195, 152, 284, 115, 7, 350, 244, 217, 259, 295, 344, 475, 139, 456, 190, 390, 18, 226, 489, 204, 233, 346, 423, 323, 367, 139, 263, 111, 235, 27, 374, 442, 155, 254, 182, 188, 330, 490, 499, 208, 424, 420, 3, 313, 498, 444, 297, 135, 298, 274, 271, 256, 53, 153, 368, 411, 331, 143, 241, 146, 429, 443, 76, 252, 364, 336, 313, 178, 28, 207, 2, 36, 289, 135, 339, 268, 485, 106, 376, 378, 281, 184, 145, 429, 44, 408, 61, 382, 411, 7, 396, 399, 155, 382, 161, 370, 149, 254, 445, 457, 109, 419, 21, 343, 122, 29, 406, 89, 296, 122, 176, 305, 199, 181, 329, 136, 298, 134, 168, 201, 484, 249, 94, 291, 42, 188, 448, 325, 409, 76, 52, 280, 471, 244, 311, 468, 170, 260, 385, 85, 40, 271, 265, 462, 495, 433, 1, 159, 380, 457, 264, 259, 491, 346, 167, 278, 41, 188, 160, 476, 438, 481, 180, 279, 46]


정렬한 후 : 
[1, 2, 2, 2, 3, 4, 7, 7, 8, 10, 11, 12, 12, 14, 15, 16, 17, 18, 18, 18, 21, 21, 22, 24, 27, 28, 28, 28, 29, 30, 30, 33, 33, 33, 36, 39, 40, 41, 41, 41, 42, 42, 43, 44, 46, 46, 46, 47, 50, 51, 52, 53, 53, 55, 56, 59, 60, 61, 61, 61, 64, 66, 68, 68, 69, 71, 76, 76, 76, 79, 80, 83, 84, 84, 85, 88, 88, 89, 90, 93, 94, 94, 98, 100, 105, 106, 109, 109, 111, 111, 114, 115, 116, 117, 119, 120, 121, 121, 122, 122, 122, 125, 125, 125, 126, 126, 128, 128, 129, 129, 134, 134, 135, 135, 135, 135, 136, 138, 138, 138, 138, 138, 139, 139, 140, 141, 143, 144, 144, 145, 146, 146, 147, 149, 149, 149, 150, 150, 152, 152, 152, 153, 154, 155, 155, 155, 156, 159, 159, 160, 161, 161, 163, 164, 165, 167, 167, 167, 168, 169, 170, 173, 173, 175, 176, 177, 178, 179, 180, 180, 181, 181, 181, 182, 183, 184, 188, 188, 188, 188, 189, 189, 189, 190, 191, 193, 195, 196, 198, 198, 199, 200, 201, 201, 202, 202, 203, 204, 204, 206, 207, 207, 208, 208, 208, 208, 210, 211, 212, 217, 217, 219, 220, 221, 221, 223, 225, 226, 226, 226, 227, 228, 228, 228, 230, 233, 235, 235, 236, 237, 239, 240, 240, 241, 244, 244, 244, 244, 246, 248, 248, 249, 249, 252, 254, 254, 255, 256, 256, 256, 258, 259, 259, 259, 260, 261, 263, 263, 264, 264, 264, 265, 265, 265, 267, 268, 268, 270, 270, 271, 271, 271, 271, 273, 274, 275, 275, 277, 278, 279, 280, 281, 282, 284, 285, 287, 288, 289, 289, 289, 291, 292, 293, 294, 295, 295, 296, 297, 298, 298, 298, 301, 301, 301, 301, 305, 305, 309, 311, 312, 313, 313, 313, 316, 318, 319, 319, 320, 321, 321, 323, 325, 325, 329, 329, 330, 331, 333, 334, 335, 335, 336, 338, 339, 339, 342, 343, 343, 343, 344, 346, 346, 346, 348, 349, 349, 350, 351, 354, 354, 355, 356, 356, 358, 360, 362, 363, 364, 366, 366, 367, 367, 368, 370, 370, 370, 371, 371, 371, 374, 374, 376, 376, 377, 378, 380, 381, 382, 382, 385, 385, 387, 387, 389, 390, 391, 392, 396, 399, 399, 399, 404, 406, 406, 406, 407, 408, 409, 410, 411, 411, 412, 413, 414, 415, 416, 416, 418, 419, 419, 420, 421, 421, 422, 422, 423, 424, 426, 427, 429, 429, 430, 431, 431, 433, 433, 437, 437, 437, 438, 438, 438, 440, 442, 442, 442, 443, 443, 444, 444, 445, 445, 447, 447, 448, 448, 449, 450, 451, 452, 455, 456, 456, 457, 457, 459, 459, 461, 462, 464, 464, 466, 466, 466, 467, 468, 468, 471, 471, 471, 473, 475, 476, 476, 477, 477, 478, 479, 479, 481, 482, 483, 484, 484, 485, 486, 489, 490, 490, 491, 494, 494, 495, 498, 498, 499, 499, 499, 499, 500]


데이터의 수 : 100
정렬 시간 : 0.027940750122070312
비교 횟수 : 499
교환 횟수 : 62734

```
## selection 과 insertion 정렬 알고리즘의 성능비교
- 선택 알고리즘 보다 삽입 알고리즘이 대체로 성능이 더 좋다.
- 그러나 삽입 알고리즘은 데이터에 따라서 최악의 경우에 성능이 크게 저하된다.
- 선택 알고리즘은 이미 정렬이 끝난 데이터들도 현재 데이터와 비교하여 가장 작은 값인지를 비교를 한다. 
- 선택 알고리즘은 비교 횟수가 크고, 교환횟수가 작다.
- 삽입 알고리즘은 비교 횟수가 작고, 교환횟수가 크다.

- 데이터수, 정렬시간, 비교횟수, 교환횟수에 대한 데이터프레임 만들기
```
summary_data = {
    "data" : [len(list), len(list_copy)],
    "sort_time" : [running_time, running_time_2],
    "compare" : [compare_counter, compare_counter_2],
    "swap" : [swap_counter, swap_counter_2]
}
```
```
df = pd.DataFrame(summary_data, columns=["data", "sort_time", "compare", "swap"],index=["selection", "insertion"])
df
=========================================
            data   sort_time   compare	 swap
selection   500    0.049870    124750    499
insertion   500	   0.027941    499       62734
```
