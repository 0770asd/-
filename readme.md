#테이블 뷰 컨트롤러
##TableViewController

앱 시작 시 기본적으로 나타낼 목록

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
