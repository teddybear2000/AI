# AI
Take drugs can be analyzed?Projects
//นับจำนวนยา
//opencv คือ library open source ที่ใช้สำหรับการประมวลภาพขั้นพื้นฐาน เช่น การเบลอภาพ การรู้จำวัตถุต่างๆในภาพ หรือการเพิ่มคุณภาพให้กับภาพ วิดีโอ 
//imutils คือ library เบื้องต้นของ image processing เช่น การหมุนภาพ กลับภาพ ปรับขนาด
//การ threshold เป็นการนำภาพ 1 channel หรือ grayscle image มาแปลงค่า intesity ของแต่ละ pixel ให้เหลือเพียง 2 ค่า คือ 0(ดำ) กับ 255(ขาว) โดยเรียกภาพที่มีค่า intensity เพียง 2 ค่า ว่า “Binary Image”
import cv2
import imutils

image = cv2.imread("pills1.jpg")
image = imutils.resize(image, width=500)
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

T, thresh = cv2.threshold(gray, 20, 255, cv2.THRESH_BINARY)
#cv2.imshow("threshold", thresh)

cnts = cv2.findContours(thresh, cv2.RETR_LIST, cv2.CHAIN_APPROX_SIMPLE)
cnts = imutils.grab_contours(cnts)
clone = image.copy()

i = 0

for c in cnts:
    # compute the area and the perimeter of the contour
    area = cv2.contourArea(c)

    if area > 0:

        i = i + 1

        cv2.drawContours(clone, [c], -1, (0, 255, 0), 2)

        M = cv2.moments(c)
        cX = int(M["m10"] / M["m00"])
        cY = int(M["m01"] / M["m00"])

        cv2.putText(clone, "#{}".format(i), (cX - 20, cY), cv2.FONT_ITALIC,
                    0.75, (204,0,0), 2)
    else:
        pass

#cv2.imshow("original", image)
cv2.imshow("counter", clone)
cv2.waitKey(0)

// บอกสีของยา color1
//PLT ย่อมาจาก “Python Imaging Library” เพิ่มการรองรับสำหรับการเปิดการจัดการและการบันทึกไฟล์รูปภาพหลายรูปแบบ
//numpy เป็นโมดูลเสริมที่มีฟังก์ชันเกี่ยวกับคณิตศาสตร์และการคำนวณต่างๆ โดยทั่วไปจะเกี่ยวกับการจัดข้อมูล arra
//matplotlib  เป็นการสร้างกราฟใน python
import cv2
from PIL import Image
import numpy as np
from matplotlib import pyplot as plt

A = Image.open("pills.jpg")
A = np.array(A)
print(A.shape)
R = A[:,:,0]
G = A[:,:,1]
B = A[:,:,2]

#cv2.imshow("A",A)
#cv2.waitKey()
#plt.subplot(2,2,1); plt.imshow(A[:,:,::-1])
plt.subplot(2,2,1); plt.imshow(A)
plt.subplot(2,2,2); plt.imshow(R, cmap='gray')
plt.subplot(2,2,3); plt.imshow(G, cmap='gray')
plt.subplot(2,2,4); plt.imshow(B, cmap='gray')
plt.show()


// บอกสีของยา color2
import cv2
import numpy

while True:

    img = cv2.imread("pills2.jpg")
    img = cv2.resize(img,(500,300))

    num = input("Enter you number :")
    if num == "1":
        lower = numpy.array([27, 5, 207])
        upper = numpy.array([43, 45, 247])

        mask = cv2.inRange(img, lower, upper)
        result = cv2.bitwise_and(img, img, mask=mask)

        cv2.imshow("Original", img)
        cv2.imshow("Result", result)

    elif num == "2":
        lower = numpy.array([72, 116, 211])
        upper = numpy.array([137, 170, 239])

        mask = cv2.inRange(img, lower, upper)
        result = cv2.bitwise_and(img, img, mask=mask)

        cv2.imshow("Original", img)
        cv2.imshow("Result", result)

    elif num == "3":
        lower = numpy.array([59, 166, 174])
        upper = numpy.array([121, 233, 228])

        mask = cv2.inRange(img, lower, upper)
        result = cv2.bitwise_and(img, img, mask=mask)

        cv2.imshow("Original", img)
        cv2.imshow("Result", result)

    elif num == "4":
        lower = numpy.array([187, 205, 216])
        upper = numpy.array([217, 228, 232])

        mask = cv2.inRange(img, lower, upper)
        result = cv2.bitwise_and(img, img, mask=mask)

        cv2.imshow("Original", img)
        cv2.imshow("Result", result)

    elif num == "5":
        lower = numpy.array([145, 144, 2])
        upper = numpy.array([193, 183, 69])

        lower2 = numpy.array([18, 1, 14])

        mask = cv2.inRange(img, lower, upper,lower2)
        result = cv2.bitwise_and(img, img, mask=mask)

        cv2.imshow("Original", img)
        cv2.imshow("Result", result)

    else:
        print("no information found")


    if cv2.waitKey(0) & 0xFF == ord("e"):
        break

cv2.destroyAllWindows()


