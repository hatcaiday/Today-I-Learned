1. Arel.sql
   Ex:
   ```
   Arel.sql("field(id, #{ids.map(&.to_i).join(', ')}))

   Arel only pass raw sql, not pass assignment variable
