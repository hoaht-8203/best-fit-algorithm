def bestFit(m, n):
    blockSize = []
    processSize = []
    allocation = [-1] * n
    holes = []  # Danh sách để lưu trữ các giá trị khoảng trống
    hole_str = ""  # Biến chuỗi để xây dựng dòng in hole

    # Nhập vào mảng blockSize
    print("Enter the block sizes:")
    for i in range(m):
        size = int(input("Block size {}: ".format(i + 1)))
        blockSize.append(size)

    # Nhập vào mảng processSize
    print("Enter the process sizes:")
    for i in range(n):
        size = int(input("Process size {}: ".format(i + 1)))
        processSize.append(size)

    for i in range(n):
        bestIdx = -1
        for j in range(m):
            if blockSize[j] >= processSize[i]:
                if bestIdx == -1:
                    bestIdx = j
                elif blockSize[bestIdx] > blockSize[j]:
                    bestIdx = j

        if bestIdx != -1:
            allocation[i] = bestIdx
            holes.append(blockSize[bestIdx])
            blockSize[bestIdx] -= processSize[i]

    print("Process No.   Process Size    Block no.")
    for i in range(n):
        print(" ", i + 1, "         ", processSize[i], "         ", end=" ")
        if allocation[i] != -1:
            print(allocation[i] + 1)
        else:
            print("Not Allocated")

    # Xây dựng dòng in hole
    for hole in holes:
        hole_str += str(hole) + " KB "

    # In ra các giá trị hole trên cùng một dòng
    print("Best-fit: :", hole_str)


# Driver code
if __name__ == '__main__':
    m = int(input("Enter the number of blocks: "))
    n = int(input("Enter the number of processes: "))

    bestFit(m, n)
