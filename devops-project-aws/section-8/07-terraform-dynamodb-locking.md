# Dynamodb for state locking

## **Problem with No State Locking**
When multiple users or processes run Terraform at the same time, several issues can arise:
1. **Concurrency Conflicts**: If two users apply changes simultaneously, they might overwrite each other's changes, leading to inconsistencies.
2. **State Corruption**: Without locking, partial updates can occur, resulting in a corrupted statefile.
3. **Unreliable Infrastructure Changes**: Race conditions can cause Terraform to misinterpret infrastructure state, leading to unintended modifications.

## **How DynamoDB Solves These Problems**
1. **State Locking**: DynamoDB creates a lock entry when Terraform applies changes, preventing concurrent modifications.
2. **Ensures Consistency**: Only one process can modify the statefile at a time, ensuring consistency and preventing corruption.
3. **Automatic Lock Release**: When Terraform execution completes, the lock entry is removed, allowing the next process to proceed.
4. **High Availability**: As a managed AWS service, DynamoDB provides reliable and scalable state locking.
5. **Cost Efficiency**: With `PAY_PER_REQUEST` billing, DynamoDB incurs minimal cost for Terraform state locking.