
# paymentlog
    import "code.whipround.net/paymentlog"




## Constants
``` go
const (
    SourceBalanced = "balanced"
    StatusPending  = "pending"
    CurrencyUSD    = "usd"
)
```

## Variables
``` go
var (
    MissingID          = errors.New("Missing payment log ID.")
    MissingAmount      = errors.New("Missing payment log amount.")
    MissingSource      = errors.New("Missing payment log source.")
    MissingSourceID    = errors.New("Missing payment log source ID.")
    MissingCreated     = errors.New("Missing payment log created timestamp.")
    MissingStatus      = errors.New("Missing payment log status.")
    MissingCurrency    = errors.New("Missing payment log currency.")
    MissingProjectID   = errors.New("Missing payment log campaign ID.")
    MissingUserID      = errors.New("Missing payment log user ID.")
    MissingAccountType = errors.New("Missing payment log account type.")
    MissingAccountID   = errors.New("Missing payment log account ID.")

    AlreadyExists = errors.New("Payment log already exists.")
    LogNotFound   = errors.New("Payment log not found.")
)
```

## func SortLogsByCreated
``` go
func SortLogsByCreated(logs []PaymentLog) []PaymentLog
```


## type FailureLog
``` go
type FailureLog struct {
    ID                string
    PaymentLogID      string
    FailureReason     string
    FailureReasonCode string
    Timestamp         time.Time
}
```










## type LogStore
``` go
type LogStore interface {
    StorePaymentLog(log PaymentLog) error
    UpdatePaymentLog(id string, change PaymentLogChange) error
    DeletePaymentLog(id string) error
    GetPaymentLog(id string) (PaymentLog, error)
    ListPaymentLogsByProject(campaignID string, num, offset int) ([]PaymentLog, error)
    ListPaymentLogsByUser(userID string, num, offset int) ([]PaymentLog, error)
    ListPaymentLogs(num, offset int) ([]PaymentLog, error)

    StoreFailureLog(failure FailureLog) error
    ListFailureLogs(num, offset int) ([]FailureLog, error)
    ListFailureLogsSince(timestamp time.Time) ([]FailureLog, error)
}
```










## type MemoryStore
``` go
type MemoryStore struct {
    sync.Mutex
    // contains filtered or unexported fields
}
```








### func NewMemoryStore
``` go
func NewMemoryStore() *MemoryStore
```



### func (\*MemoryStore) DeletePaymentLog
``` go
func (store *MemoryStore) DeletePaymentLog(id string) error
```


### func (\*MemoryStore) GetPaymentLog
``` go
func (store *MemoryStore) GetPaymentLog(id string) (PaymentLog, error)
```


### func (\*MemoryStore) ListPaymentLogsByProject
``` go
func (store *MemoryStore) ListPaymentLogsByProject(id string, num, offset int) ([]PaymentLog, error)
```


### func (\*MemoryStore) StorePaymentLog
``` go
func (store *MemoryStore) StorePaymentLog(log PaymentLog) error
```


### func (\*MemoryStore) UpdatePaymentLog
``` go
func (store *MemoryStore) UpdatePaymentLog(id string, change PaymentLogChange) error
```


## type PaymentLog
``` go
type PaymentLog struct {
    ID          string
    Amount      uint
    Description string
    Source      string
    SourceID    string
    Created     time.Time
    Updated     time.Time
    Status      string
    Currency    string
    ProjectID   string
    UserID      string
    AccountID   string
    AccountType string
}
```










### func (PaymentLog) Validate
``` go
func (p PaymentLog) Validate() error
```


## type PaymentLogChange
``` go
type PaymentLogChange struct {
    Amount      *uint
    Description *string
    Source      *string
    SourceID    *string
    Created     *time.Time
    Updated     *time.Time
    Status      *string
    Currency    *string
}
```
















- - -
Generated by [godoc2md](http://godoc.org/github.com/davecheney/godoc2md)