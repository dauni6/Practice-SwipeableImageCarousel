원본 글 : https://proandroiddev.com/swipeable-image-carousel-with-smooth-animations-in-jetpack-compose-76eacdc89bfb

lerp는 두 DP값 사이를 선형 보간한다. 
선형 보간은 시작 값과 종료 값 사이의 중간 값을 주어진 분수(일반적으로 0과 1 사이의 값)에 따라 계산하며 공식은 다음과 같다.

**lerp(start, stop, fraction) = start + (stop - start) * fraction**

fraction이 0일 때 결과는 start이다.

fraction이 1일 때 결과는 stop이다.

fraction이 0과 1 사이의 값이면 결과는 start와 stop 사이에 비례하여 계산된 값이다.

예를 들어:

```
lerp(
    start = 75.dp,
    stop = 100.dp,
    fraction = 1f - pageOffset.coerceIn(0f, 1f)
).also { scale ->
    scaleY = scale / 100.dp
}
```
start = 75.dp: 최소 스케일 값 (75 밀도 독립 픽셀)

stop = 100.dp: 최대 스케일 값 (100 밀도 독립 픽셀)이 된다.

**fraction = 1f — pageOffset.coerceIn(0f, 1f)**:

pageOffset은 현재 페이지가 HorizontalPager에서 완전히 중앙에 오기까지 얼마나 떨어져 있는지를 나타내며, 0에서 1 이상의 범위를 가질 수 있다. 하지만 coerceIn(0f, 1f)을 통해 0과 1 사이로 제한된다.

1f — pageOffset은 이 값을 반전시킨다. 즉, 페이지가 완전히 중앙에 있으면(pageOffset = 0) fraction은 1이 되고, 페이지가 완전히 화면에서 벗어나면(pageOffset = 1) fraction은 0이 된다.

lerp 결과:
결과적으로 75.dp와 100.dp 사이에서 부드러운 전환이 이루어짐.

예를 들어:

fraction = 1 (페이지가 중앙에 있을 때), 결과는 100.dp

fraction = 0 (페이지가 완전히 벗어났을 때), 결과는 75.dp

fraction = 0.5 (중간일 때), 결과는 87.5.dp이 된다.
