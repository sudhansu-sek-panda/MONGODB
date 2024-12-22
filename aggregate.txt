use usbm
switched to db usbm
db.createCollection("customers")
{ ok: 1 }
show collections
customers
student
db.customers.find()
db.customers.insertMany([
  { "cust_id": "C001", "status": "A", "amount": 100 },
  { "cust_id": "C002", "status": "A", "amount": 200 },
  { "cust_id": "C001", "status": "B", "amount": 50 },
  { "cust_id": "C003", "status": "A", "amount": 150 }
]
)
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('67683adeabe2af1d1412f3e4'),
    '1': ObjectId('67683adeabe2af1d1412f3e5'),
    '2': ObjectId('67683adeabe2af1d1412f3e6'),
    '3': ObjectId('67683adeabe2af1d1412f3e7')
  }
}
db.customers.find()
{
  _id: ObjectId('67683adeabe2af1d1412f3e4'),
  cust_id: 'C001',
  status: 'A',
  amount: 100
}
{
  _id: ObjectId('67683adeabe2af1d1412f3e5'),
  cust_id: 'C002',
  status: 'A',
  amount: 200
}
{
  _id: ObjectId('67683adeabe2af1d1412f3e6'),
  cust_id: 'C001',
  status: 'B',
  amount: 50
}
{
  _id: ObjectId('67683adeabe2af1d1412f3e7'),
  cust_id: 'C003',
  status: 'A',
  amount: 150
}
db.customers.find().pretty()
db.customers.aggregate([
  {$match: {status: "A"}},
  {$group: {_id: "$cust_id", total: {$sum: "$amount"}}},
  {$sort: {total: -1}}
])
{
  _id: 'C002',
  total: 200
}
{
  _id: 'C003',
  total: 150
}
{
  _id: 'C001',
  total: 100
}