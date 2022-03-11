## mvvm 스터디 2주차



#### recyclerView

+ recyclerView는 꼭 layoutmanager 지정해줘야 함

+ recyclerView의 Adapter 지금까지는 `RecyclerView.Adapter` 상속 받아서 직접 구현을 해줬음 

+ ListAdapter를 활용해서 Adapter를 만들기 

  + List의 변경점이 생겼을 때, 이를 View에 알려줘야 하는데, 일일이 notify 쓰지 않아도 ListAdapter를 쓰면 이를 할 필요가 없음

  + 성능이 좋음(DiffUtil)

  + 단점 

    + 비교할 아이템마다 diffutil을 일일이 만들어줘야 함

    + 복잡한 리스트의 갱신이 있으면 다음 상태의 리스트를 직접 만들어줘야 함. 리스트 순서 조작을 수동으로 해야될 수도 있음 .

```kotlin
class DiariesAdapter(
private val onDiaryClick: ((Diary) -> Unit)? = null,
) : ListAdapter<Diary, DiariesAdapter.ViewHolder>(DiariesComparator()) {
    
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        val layoutInflator = LayoutInflator.from(parent.context)
        val binding = ItemDiaryBinding.inflate(layoutInflater, parent, false)
        return ViewHolder(binding)
    }
    
    override fun onBindViewHolder(holder: ViewHolder, position: Int){
        val diary: Diary = getItem(position)
        holder.bind(diary, onDiaryClick)
    }
    
   
    class ViewHolder(
    	private val binding: ItemDiaryBinding,
    ) : RecyclerView.ViewHolder(binding.root){
        
        fun bind(dairy: Diary, onDiaryClick: ((Diary) -> Unit) ?= null) {
            binding.diary = diary
            binding.root.setOnClickListener {onDiaryClick?.invoke(diary)}
        }
    }
    
    // diary라는 아이템을 고유하게 비교해주는 diffUtil => 리사이클러뷰한테 이 diary는 이렇게 비교해 ~ 라고 알려주는 것
    private class DiariesComparator: DiffUtil.ItemCallback<Diary>(){
        // ctrl+i 누르면 구현해야 할 method들 띄워줌
        override fun areItemsTheSame(oldItem: Diary, newItem: Diary): Boolean {
            return oldItem.id == newItem.id
        }
        
        override fun areContentsTheSame(oldItem: Diary, newItem: Diary): Boolean {
            return oldItem == newItem
        }
    }
}
```

+ diary라는 아이템을 고유하게 비교해주는 diffUtil

+ 이 diary라는 item이 서로 고유하게 같은지 다른지를 check하기 위해 areItemsTheSame을 먼저 호출하고 이 method가 true를 반환하면 다음에 areContentsTheSame을 호출해서 또 비교함. 

  => 두 아이템이 교유하게 id로써 같아도 content가 다를 수도 있음

+ data를 받아서 보여주는 것은 ListAdapter가 다 해줌. 우리가 data를 넘기는 것은 recyclerView 사용하는 Activity 파일에서 `submitList` method로 가능

<br>

Activity에서 ListAdapter 사용 

```kotlin
class DiariesActivity : AppCompatActivity() {
    private lateinit var binding: ActivityDiariesBinding
    private lateinit var diariesAdapter: DiariesAdapter
    
    override fun onCreate(~){
        super.onCreate(~)
        
        diariesAdapter = DiariesAdapter {onDiaryClick(it)}
        
        binding.listDiaries.adapter = diariesAdapter
        
        diariesAdapter.submitList(STUB_DIARY)
        // 이 코드는 비동기적으로 실행 
    }
    
    private fun onDiaryClick(diary: Diary){
        val intent = Intent(this, EditDiaryActivity::class.java)
        startActivity(intent)
    }
    
    companion object {
        private val STUB_DIARY = listOf(
            Diary("0", "title", "content", Date()),
            Diary("1", "title", "content", Date()),
            Diary("2", "title", "content", Date()),
            Diary("3", "title", "content", Date()),
            Diary("0", "title", "content", Date()),
            Diary("0", "title", "content", Date()),
        )
    }
}
```

+ `diariesAdapter.submitList(STUB_DIARY)` : 이 코드는 비동기적으로 실행된다.

  => 따라서, 위 submitList의 작업이 다 끝나고 무엇인가를 실행하고 싶다면 

  `diariesAdapter.submitList(STUB_DIARY) {  ~  }` 이렇게 중괄호 안에 비동기 실행 이후 동작하기를 원하는 코드를 작성하면 됨.



+ 

// 1:20:00 ~