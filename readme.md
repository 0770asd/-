# 테이블 뷰 컨트롤러
## TableViewController

### 앱 시작 시 기본적으로 나타낼 목록

```javascript
import UIKit
 
var items = ["책 구매", "철수와 약속", "스터디 준비하기"]
var itemsImageFile = ["cart.jpeg", "clock.jpeg", "pencil.jpeg"]
 
class TableViewController: UITableViewController {

    @IBOutlet var tvListView: UITableView!

    override func viewDidLoad() {
        super.viewDidLoad()

        // Uncomment the following line to preserve selection between presentations
        // self.clearsSelectionOnViewWillAppear = false

        // Uncomment the following line to display an Edit button in the navigation bar for this view controller.
        self.navigationItem.leftBarButtonItem = self.editButtonItem
    }
```


### 뷰가 노출될 때마다 리스트의 데이터를 다시 불러옴

```javascript
override func viewWillAppear(_ animated: Bool) {
        tvListView.reloadData()
    }
    ```


### 테이블 안의 섹션 개수를 1로 설정함

```javascript
// MARK: - Table view data source
    override func numberOfSections(in tableView: UITableView) -> Int {
        // #warning Incomplete implementation, return the number of sections
        return 1
    }
    ```


### 섹션당 열의 개수를 전달

```javascript
 override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        // #warning Incomplete implementation, return the number of rows
        return items.count
    }
```


### item와 itemslmageFile의 값을 셀에 삽입함

```javascript
override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "myCell", for: indexPath)

        cell.textLabel?.text = items[(indexPath as NSIndexPath).row]
        cell.imageView?.image = UIImage(named: itemsImageFile[(indexPath as NSIndexPath).row])

        return cell
    }
```


### 목록 삭제 함수

```javascript
 // Override to support editing the table view.
    override func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath) {
        if editingStyle == .delete {
```


### item와 itemslmageFile에 해당 리스트를 삭제함 

```javascript
items.remove(at: (indexPath as NSIndexPath).row)
            itemsImageFile.remove(at: (indexPath as NSIndexPath).row)
            tableView.deleteRows(at: [indexPath], with: .fade)
        } else if editingStyle == .insert {
            // Create a new instance of the appropriate class, insert it into the array, and add a new row to the table view
        }    
    }
```


### 삭제 시 "Delete" 대신 "삭제" 로 표시

```javascript
override func tableView(_ tableVeiw: UITableView, titleForDeleteConfirmationButtonForRowAt indexPath: IndexPath) -> String? {
        return "삭제"
    }
```


### 목록 순서 바꾸기

```javascript
 // Override to support rearranging the table view.
    override func tableView(_ tableView: UITableView, moveRowAt fromIndexPath: IndexPath, to: IndexPath) {
        let itemToMove = items[(fromIndexPath as NSIndexPath).row]
        let itemImageToMove = itemsImageFile[(fromIndexPath as NSIndexPath).row]
        items.remove(at: (fromIndexPath as NSIndexPath).row)
        itemsImageFile.remove(at: (fromIndexPath as NSIndexPath).row)
        items.insert(itemToMove, at: (to as NSIndexPath).row)
        itemsImageFile.insert(itemImageToMove, at: (to as NSIndexPath).row)
    }
```    
 
 
### 세그웨이를 이용하여 디테일 뷰로 전환하기

```javascript
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        // Get the new view controller using segue.destination.
        // Pass the selected object to the new view controller.
        if segue.identifier == "sgDetail" {
            let cell = sender as! UITableViewCell
            let indexPath = self.tvListView.indexPath(for: cell)
            let detailView = segue.destination as! DetailViewController
            detailView.receiveItem(items[((indexPath! as NSIndexPath).row)])
    }

} 

}
```


## AddViewController

### 텍스트 필드 함수 지정

```javascript
mport UIKit

class AddViewController: UIViewController {

    @IBOutlet var tfAddItem: UITextField!

    override func viewDidLoad() {
        super.viewDidLoad()

        // Do any additional setup after loading the view.

    }
```    


### 새 목록 추가하기

```javascript
@IBAction func btnAddItem(_ sender: UIButton) {
        items.append(tfAddItem.text!)
        itemsImageFile.append("clock.jpeg")
        tfAddItem.text=""
        _ = navigationController?.popViewController(animated: true)
    }
```


## DetailViewConTroller

### Main View에서 변수를 받아오기 위한 함수

```javascript
func receiveItem(_ item: String)

    {
        receiveItem = item
    }
```

<img src="https://user-images.githubusercontent.com/106363908/174153969-39e2e4df-b34b-4652-b247-e6011d9498de.png" width="100" height="100">



