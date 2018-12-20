1. canvas是一个html标签。

2. 有两个属性：width，height。默认宽高为300*150

3. 当你想使用任何新东西时，兼容性是不得不考虑的一个东西。在不支持canvas的浏览器，canvas支持替换内容。

4. canvas元素需要结束标签`</canvas>`。如果结束标签不存在，则文档的其余部分会被认为是替代内容，将不会显示出来。

5. canvas起初是空白的。为了展示，首先脚本需要找到渲染上下文，然后在它的上面绘制。

6. canvas元素有一个叫做 `getContext()` 的方法，这个方法是用来获得渲染上下文和它的绘画功能。getContext()只有一个参数，上下文的格式。
    ```
        var canvas = document.getElementById('id');
        var ctx = canvas.getContext('2d');
    ```

7. 栅格（canvas grid）:canvas元素默认被网格所覆盖。通常来说网格中的一个单元相当于canvas元素中的一像素。栅格的起点为左上角（坐标为（0,0））。所有元素的位置都相对于原点定位。

8. canvas只支持一种原生的图形绘制：矩形。所有其他的图形的绘制都至少需要生成一条路径。

9. canvas提供了三种方法绘制矩形：
    ```
        fillRect(x, y, width, height)
        // 绘制一个填充的矩形
        strokeRect(x, y, width, height)
        // 绘制一个矩形的边框
        clearRect(x, y, width, height)
        // 清除指定矩形区域，让清除部分完全透明。
    ```
    > 上面提供的方法之中每一个都包含了相同的参数。x与y指定了在canvas画布上所绘制的矩形的左上角（相对于原点）的坐标。width和height设置矩形的尺寸。

10. 绘制路径:图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。一个路径，甚至一个子路径，都是闭合的。`haohoaduzhejuhua`

11. 使用路径绘制图形需要一些额外的步骤。
    > 首先，你需要创建路径起始点。

    > 然后你使用画图命令去画出路径。
    
    > 之后你把路径封闭。
    
    > 一旦路径生成，你就能通过描边或填充路径区域来渲染图形。

12. 以下是所要用到的函数：
    - `beginPath()`新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径。
    - `closePath()`闭合路径之后图形绘制命令又重新指向到上下文中。
    - `stroke()`通过线条来绘制图形轮廓。
    - `fill()`通过填充路径的内容区域生成实心的图形。

13. 路径是由很多子路径构成，这些子路径都是在一个列表中，所有的子路径（线、弧形、等等）构成图形。而每次这个方法调用之后，列表清空重置，然后我们就可以重新绘制新的图形。
    > 当前路径为空，即调用beginPath()之后，或者canvas刚建的时候，第一条路径构造命令通常被视为是moveTo（），无论实际上是什么。出于这个原因，你几乎总是要在设置路径之后专门指定你的起始位置。

14. 当你调用fill()函数时，所有没有闭合的形状都会自动闭合，所以你不需要调用closePath()函数。但是调用stroke()时不会自动闭合。

15. `moveTo(x, y)`:将笔触移动到指定的坐标x以及y上。

16. `lineTo(x, y)`:绘制一条从当前位置到指定x以及y位置的直线。

17. `arc(x, y, radius, startAngle, endAngle, anticlockwise)`：画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成。
    - x,y为绘制圆弧所在圆上的圆心坐标。
    - radius为半径。
    - startAngle以及endAngle参数用弧度定义了开始以及结束的弧度。这些都是以x轴为基准。
    - 参数anticlockwise为一个布尔值。为true时，是逆时针方向，否则顺时针方向。
    > arc( )函数中表示角的单位是弧度，不是角度。角度与弧度的js表达式：`弧度=(Math.PI/180)*角度。`

18. `arcTo(x1, y1, x2, y2, radius)`：根据给定的控制点和半径画一段圆弧，再以直线连接两个控制点。

19. `rect(x, y, width, height)`：绘制一个左上角坐标为（x,y），宽高为width以及height的矩形。
    > 当该方法执行的时候，moveTo()方法自动设置坐标参数（0,0）。也就是说，当前笔触自动重置回默认坐标。
20. `fillStyle` 和 `strokeStyle`：
    > fillStyle = color :设置图形的填充颜色。

    > strokeStyle = color :设置图形轮廓的颜色。

    > 一旦设置了 strokeStyle 或者 fillStyle 的值，那么这个新值就会成为新绘制的图形的默认值。如果要给每个图形上不同的颜色，需要重新设置 fillStyle 或 strokeStyle 的值。

21. `globalAlpha = transparencyValue`：这个属性影响到 canvas 里所有图形的透明度，有效的值范围是 0.0 （完全透明）到 1.0（完全不透明），默认是 1.0。
    > strokeStyle 和 fillStyle 属性接受符合 CSS 3 规范的颜色值，那我们可以用下面的写法来设置具有透明度的颜色。
    ```
        ctx.strokeStyle = "rgba(255,0,0,0.5)";
        ctx.fillStyle = "rgba(255,0,0,0.5)";
    ```

22. 线型（Line styles）：
    - lineWidth = value：设置线条宽度。

    - lineCap = type：设置线条末端样式。
        > lineCap 的值决定了线段端点显示的样子。它可以为下面的三种的其中之一：butt，round 和 square。默认是 butt。

    - lineJoin = type：设定线条与线条间接合处的样式。
        > lineJoin 的属性值决定了图形中两线段连接处所显示的样子。它可以是这三种之一：round, bevel 和 miter。默认是 miter。

    - miterLimit = value：限制当两条线相交时交接处最大长度；所谓交接处长度（斜接长度）是指线条交接处内角顶点到外角顶点的长度。

    - getLineDash()：返回一个包含当前虚线样式，长度为非负偶数的数组。

    - setLineDash(segments)：设置当前虚线样式。

    - lineDashOffset = value：设置虚线样式的起始偏移量。