# Policy structure

{
  "Statement": [{
    "Effect":"effect",
    "Action":"action",
    "Resource":"arn",
    "Condition":{
      "condition":{
        "key":"value"
        }
      }
    }
  ]
}

* Effect: The effect can be Allow or Deny.
* Action: The action is the specific API action
* Resource: Amazon Resource Name (ARN)