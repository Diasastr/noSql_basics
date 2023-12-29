# Завдання "База Даних Спортзалу"

Цей репозиторій містить код та інструкції для виконання завдання "База Даних Спортзалу". 

- Комп'ютер з операційною системою Windows та встановленим Chocolatey.

## Крок 1: Встановлення MongoDB

1. Відкрийте командний рядок в режимі адміністратора.

2. Встановіть MongoDB за допомогою Chocolatey:
   ```shell
   choco install mongodb
   ```
   Також є сенс встановити MongoDB Shell з їх офіційного вебсайту :)

4. Запустіть службу MongoDB (монго шел).

## Крок 2: Створення Бази Даних та Колекцій

1. В оболонці MongoDB створіть базу даних "gymDatabase".
   
   ```shell
   use gymDatabase
   ```
   
3. Створіть колекції: "clients" (клієнти), "memberships" (членства), "workouts" (тренування), "trainers" (тренери).

   ```shell
   db.createCollection("clients")
   db.createCollection("memberships")
   db.createCollection("workouts")
   db.createCollection("trainers")
   ```
   Вивід:

   ```mongo
   db.createCollection("clients")
   { ok: 1 }
   gymDatabase> db.createCollection("memberships")
   { ok: 1 }
   gymDatabase> db.createCollection("workouts")
   { ok: 1 }
   gymDatabase> db.createCollection("trainers")
   { ok: 1 }
   ```

   
## Крок 3: Додавання Даних

Додайте дані в колекції.

   ```mongo
   db.clients.insertMany([
    { client_id: "c2", name: "Alice Johnson", age: 30, email: "alicej@example.com" },
    { client_id: "c3", name: "Michael Brown", age: 22, email: "michaelb@example.com" },
    { client_id: "c4", name: "Emma Wilson", age: 28, email: "emmaw@example.com" }
   ])

   db.memberships.insertMany([
    { membership_id: "m2", client_id: "c2", start_date: new Date("2023-02-01"), end_date: new Date("2024-01-31"), type: "Annual" },
    { membership_id: "m3", client_id: "c3", start_date: new Date("2023-03-01"), end_date: new Date("2023-09-30"), type: "Half-Year" },
    { membership_id: "m4", client_id: "c4", start_date: new Date("2023-04-01"), end_date: new Date("2023-04-30"), type: "Monthly" }
   ])

   db.workouts.insertMany([
    { workout_id: "w2", description: "Strength Training", difficulty: "Hard" },
    { workout_id: "w3", description: "Yoga Session", difficulty: "Easy" },
    { workout_id: "w4", description: "HIIT", difficulty: "Hard" }
   ])

   db.trainers.insertMany([
    { trainer_id: "t2", name: "Lucas Green", specialization: "Strength Training" },
    { trainer_id: "t3", name: "Sophia Lee", specialization: "Yoga" },
    { trainer_id: "t4", name: "Ethan Hall", specialization: "HIIT" }
   ])
   ```
   etc...

   Вивід:

   ```mongo
   db.clients.insertMany([ { client_id: "c2", name: "Alice Johnson", age: 30, email: "alicej@example.com" }, { client_id: "c3", name: "Michael Brown", age: 22, email: "michaelb@example.com" }, { client_id: "c4", name: "Emma Wilson", age: 28, email: "emmaw@example.com" }])
    {
      acknowledged: true,
      insertedIds: {
        '0': ObjectId('658f45a3456998b840766d5d'),
        '1': ObjectId('658f45a3456998b840766d5e'),
        '2': ObjectId('658f45a3456998b840766d5f')
      }
    } 1 }
   ```
  and so on...

# Крок 4: Запити

1. Виконуйте запити до даних.

   - Знайти клієнтів старше 30 років.
     
     ```mongo
     db.clients.find({ age: { $gt: 30 } })
     ```
     Вивід:

     ```mongo
      [
        {
          _id: ObjectId('658f480e456998b840766d69'),
          client_id: 'c5',
          name: 'Oliver Davis',
          age: 35,
          email: 'oliverd@example.com'
        }
      ]
     ```


   - Перелічити тренування з середньою складністю.
     
     ```mongo
     db.workouts.find({ difficulty: "Medium" })
     ```
     Вивід:
  
     ```mongo
     db.workouts.find({ difficulty: "Medium" })
      [
        {
          _id: ObjectId('658f4860456998b840766d6e'),
          workout_id: 'w7',
          description: 'Intermediate Yoga Session',
          difficulty: 'Medium'
        },
        {
          _id: ObjectId('658f4860456998b840766d6f'),
          workout_id: 'w8',
          description: 'Moderate HIIT',
          difficulty: 'Medium'
        }
      ]
      gymDatabase> db.memberships.findOne({ client_id: "c2" })
      {
        _id: ObjectId('658f471d456998b840766d60'),
        membership_id: 'm2',
        client_id: 'c2',
        start_date: ISODate('2023-02-01T00:00:00.000Z'),
        end_date: ISODate('2024-01-31T00:00:00.000Z'),
        type: 'Annual'
      }
     ```

   - Показати інформацію про членство для певного клієнта.

     ```mongo
     db.memberships.findOne({ client_id: "c2" })
     ```
     Вивід:
  
     ```mongo
     {
      _id: ObjectId('658f471d456998b840766d60'),
      membership_id: 'm2',
      client_id: 'c2',
      start_date: ISODate('2023-02-01T00:00:00.000Z'),
      end_date: ISODate('2024-01-31T00:00:00.000Z'),
      type: 'Annual'
     }
     ```
   
