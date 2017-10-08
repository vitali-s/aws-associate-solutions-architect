# Delete markers

* It does not have data associated with it.
* It is not associated with an access control list (ACL) value.
* It does not retrieve anything from a GET request because it has no data; you get a 404 error.
* The only operation you can use on a delete marker is DELETE, and only the bucket owner can issue such a request.

Identification of Delete marker:
* A 404 (Object not found) error
* A response header, x-amz-delete-marker: true

The only way to get delete merkers is to list all versions.

Delete marker:
* Delete version id, which is delete marker