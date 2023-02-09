# Vector常用方法

```c#
Debug.Log(Vector3.Angle(v,v2));  //计算两个向量夹角
Debug.Log(Vector3.Distance(v,v2));//计算两个点之间的距离
Debug.Log(Vector3.Dot(v,v2));//点乘
Debug.Log(Vector3.Cross(v,v2));//叉乘
Debug.Log(Vector.Lerp(Vector3.zero,Vector.one,0.5f));//插值
Debug.Log(v.magnitude);//向量的模
Debug.Log(v.nomalized);//规范化向量

//旋转：欧拉角，四元数

Vector3 rotate =new Vector3(0,30,0);
Quaternion quaternion= Quaternion.identity;
//欧拉角转化成四元数
quaternion=Quaternion.Euler(rotate）；
//四元数转化为欧拉角
v = quaternion.eulerAngles;
//看向一个物体
quaternion = Quaternion.LookRotation(Vector3.zero);               


```

# Debug

```
Debug.Log("text");
Debug.LogWarning("text2"); //警告
Debug.LogError("text");    //错误输出
Debug.DrawLine(Vector3.zero,Vector.one,Color.bule); //划线（调试方法） 起点 终点 颜色
Debug.DrawRay(Vector3.zero,Vector3.up,Color.red);	//起点，射线，颜色




```



#  GameObject类物体移动

```
//拿到当前脚本所挂载的游戏物体

//GameObject go =this.gameObject; 
//名称
Debug.Log(gameObject.name); 
//tag
Debug.Log(gameObject.tag); 
//layer
Debug.Log(gameObject.layer); 
//立方体的名称

Debug.Log(Cube.name); 
//当前真正的激活状态

Debug.Log(Cube.activelnHierarchy); 
//当前自身激活状态

Debug.Log(Cube.activeSelf); 
```

# 拿到预设体实例化游戏物体

```c#
BoxCollider bc =GetComponent<BoxCollider>()); 
／／获取当前物体的子物体身上的某个组件
//GetComponentInChildren<CapsuleCollider>(bc); 
／／获取当前物体的父物体身上的某个组件
//GetComponentlnParent<BoxCollider>0); 
／／添加一个组件
Cube.AddComponent<AudioSource>0);
／／通过游戏物体的名称来获取游戏物体
GameObject test =GameObject.Find("Test");
／／通过游戏标签来获取游戏物体
test = GameObject.FindWithTag("Enemy"); 
test.SetActive(false);
Debug.Log(test.name); 



GameObject go=instantiate(预设体名称); //创造实例
GameObject go= Instantiate(prefab,Vector3.one,Quaternion.identity);
Destroy(go);//销毁
```



# 游戏时间使用

```c#
Debug.Log(Time.time); //游戏开始到现在的时间
Debug.Log(Time.timeScale) //时间缩放值
Debug.Log(Time.fixdDeltaTime);//固定时间间隔
Debug.Log(Time.deltaTime);//上一帧到这一帧所用的时间

```

# Application类

```
／／游戏数据文件夹路径（只读，加密压缩）

Debug.Log（Application.dataPath＋＂／新建文本文档.txt＂）； 
／／持久化文件夹路径
Debug.Log(Application.persistentDataPath); 
／／StreamingAssets文件夹路径（只读，配置文件） Debug.Log(Application.streamingAssetsPath); 
／／临时文件夹
Debug.Log(Application.temporaryCachePath);
／／控制是否在后台运行
Debug.Log(Application.runlnBackground); 
／／打开url
Application.OpenURL(""); 
//退出游戏
Application.Quit();

```

# 场景类，场景管理类 SceneManger

```c#
//加载场景
SceneManger.LoadScene();
／／获取当前场景
Scene scene =SceneManager.GetActiveScene(); 
／／场景名称
Debug.Log(scene.name); 
／／场景是否已经加载
Debug.Log(scene.isLoaded);
／／场景路径
Debug.Log(scene.path); 
／／场景索引
Debug.Log(scene.buildlndex);
GameObject[] gos =scene.GetRootGameObjects(); 
Debug.Log(gos.Length);



//场景管理类
Scene newScene =SceneManager.CreateScene("newScene"); 
／／已加载场景个数
Debug.Log(SceneManager.sceneCount); 
／／卸载场景
SceneManager.UnloadSceneAsync(newScene); 
／／加载场景
//Single关闭所有当前加载的场景 并加载一个场景。Additive将场景添加到当前加载的场景。
SceneManager.LoadScene("MyScene",LoadSceneMode.Additive); 

```

# 异步加载场景

```c#
//协程方法
public class AsyncTest:MonoBehaviour
{
	AsyncOperation operation;
	void Start(){
    StartCoroutine(loadScene());
	} 
／／协程方法用来异步加载场景1个引用
	IEnumerator loadScene() {
	operation =SceneManager.LoadSceneAsync(1); 
    ／／加载完场景不要自动跳转
	operation.allowSceneActivation =false; 
	yield return operation;
	} 
    void Update(){
	／／输出加载进度0—0.9
	Debug.Log(operation.progress); timer += Time.deltaTime; ／／如果到达5秒，再跳转
	if (timer > 5) {
	operation.allowSceneActivation =true;
	}
    }
}
```

# Transform位置 旋转 缩放 父子组件控制

```c#
//获取位置
Debug.Log(transform.position); Debug.Log(transform.localPosition); 
//获取旋转
Debug.Log(transform.rotation); Debug.Log(transform.localRotation); Debug.Log(transform.eulerAngles); Debug.Log(transform.localEulerAngles); 
//获取缩放
Debug.Log(transform.localScale); 
//向量
Debug.Log(transform.forward); Debug.Log(transform.right); Debug.Log(transform.up);


//时时刻刻看向000点
transform.LookAt(Vector3.zero); 
//旋转
transform.Rotate(Vector3.up, 1); 
//绕某个物体旋转
transform.RotateAround(Vector3.zero, Vector3.up, 5); //移动
transform.Translate(Vector3.forward* 0.1f); 


／／父子关系
／／获取父物体
transform.parent.gameObject 
／／子物体个数
Debug.Log(transform.childCount); 
／／解除与子物体的父子关系
transform.DetachChildren(); 
／／获取子物体
Transform trans = transform.Find("Child"); 
trans =transform.GetChild(0);
判断一个物体是不是另外一个物体的子物体
bool res= trans.lsChildOf(transform); Debug.Log(res);
／／设置为父物体
trans.SetParent(transform); 

```

# 键鼠操作（在update中写）

111
2222
wfasd
