 原文链接：https://www.cnblogs.com/Damon-3707/p/11268133.html
 
 - 成员变量:

        position：在世界空间坐标transform的位置。

        localPosition：相对于父级的变换的位置。如果该变换没有父级，那么等同于Transform.position。

        eulerAngles：世界坐标系中的旋转（欧拉角）。

        localEulerAngles：相对于父级的变换旋转角度。

        right：世界坐标系中的右方向。（世界空间坐标变换
        的红色轴。也就是x轴。）

        up：世界坐标系中的上方向。（在世界空间坐标变换的绿色轴。也就是y轴。）

        forward：世界坐标系中的前方向。（在世界空间坐标变换的蓝色轴。也就是z轴。）

        rotation：世界坐标系中的旋转（四元数）。

        localRotation：相对于父级的变换旋转角度。

        localScale：相对于父级的缩放比例。

        parent：父对象Transform组件。

        worldToLocalMatrix：矩阵变换的点从世界坐标转为自身坐标（只读）。

        localToWorldMatrix：矩阵变换的点从自身坐标转为世界坐标（只读）。

        root：对象层级关系中的根对象的Transform组件。

        childCount：子对象数量。

        lossyScale：全局缩放比例（只读）。

- 成员函数：

        1、LookAt函数
        public void LookAt(Transform target)

        public void LookAt(Vector3 worldPosition);

        public void LookAt(Vector3 worldPosition, 
        Vector3 worldUp = Vector3.up);

        public void LookAt(Transform target, Vector3 worldUp = Vector3.up);

        旋转物体，使物体的z轴指向target/worldPosition，对于worldUp的描述是，在完成上面的旋转之后，继续旋转自身，使得当前对象的正y轴朝向与worldUp所指向的朝向一致。
        这里的朝向一致指的是新旋转后的y轴与worldUp在该对象初次旋转后的xy平面上的投影向量一致。之所以取投影是因为第一次旋转使物体的z轴指向target/worldPosition后，此时的worldUp向量可能不在xy平面上，要在z轴指向target/worldPosition前提下是y轴朝向与worldUp一致，只能取worldUp在xy平面上的投影。
        注意：使用worldPosition向量时要注意方向，一定是target-transform.position，顺序反了会使物体背向目标；若使用Transform作为参数，则不必注意。默认情况下，worldUp是Vector3.up（世界坐标系下的y轴）

        2、Rotate函数
        public void Rotate(Vector3 eulerAngles);

        public void Rotate(Vector3 eulerAngles, 
        Space relativeTo = Space.Self);

        public void Rotate(float xAngle, float yAngle, float zAngle);

        public void Rotate(float xAngle, float yAngle, float zAngle, Space relativeTo = Space.Self);
        旋转一个欧拉角度，它按照zxy的顺序进行旋转，默认情况下局部坐标系下Space.Self

        public void Rotate(Vector3 axis, float angle);
        public void Rotate(Vector3 axis, float angle,Space relativeTo = Space.Self);
        绕axis轴旋转angle角度，默认情况下局部坐标系下Space.Self。
        transform.rotation和Rotate有个区别：
        Rotate()方法是：旋转多少度。在原有的基础上累加，即旋转了多少角度。又旋转了多少角度，是在原有的基础上在旋转
        rotation属性是：旋转到某个角度，就是是在update中每帧都执行。但每次旋转到的角度都是5，所以是旋转到5度。一直都是
        比如你只想让他旋转到多少, 用rotation; 假如想让他一直转,可以用Rotate
        rotation直接改变了数值, 以达到旋转效果
        Rotate应用一个的旋转角度每秒1度慢慢的旋转物体
        当然:rotation()还可以通过插值旋转