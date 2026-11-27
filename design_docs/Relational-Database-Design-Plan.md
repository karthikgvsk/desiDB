# Relational Database — Design Plan

## Requirements

### Functional Requirements

1. **Create table**
   - Users should be able to create a table.
   - Users should be able to specify the primary key and other columns.
   - Initially, only string columns will be supported.

2. **Insert**
   - Users should be able to provide an SQL `INSERT` command.
   - The system should parse the command and insert the record.
   - Limits and constraints for the `INSERT` command will be specified separately.

3. **Update**
   - Users should be able to provide an SQL `UPDATE` command.
   - The system should parse the command and update the record.
   - Limits and constraints for the `UPDATE` command will be specified separately.

4. **Delete**
   - Users should be able to provide an SQL `DELETE` command.
   - The system should parse the command and delete the record.
   - Limits and constraints for the `DELETE` command will be specified separately.

5. **Select**
   - Users should be able to run an SQL `SELECT` command.
   - The initial implementation should support a `WHERE` clause.

## Design
