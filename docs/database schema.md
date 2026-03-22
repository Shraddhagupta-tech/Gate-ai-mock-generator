User
- id int auto-increment primary key
- name varchar(50) not null
- email varchar(50) unique
- password_hash varchar(255) not null
- role (student/admin) default student
- created_at timestamp default current_timestamp
- updated_at timestamp default current_timestamp

Concept
- id int primary key
- concept_code varchar(50) unique
- subject varchar(50) not null
- topic varchar(50) not null
- subtopic
- difficulty_level enum(easy/medium/hard) 
- exam enum(CSE / DA)
- weightage 

Question
- id int primary key
- template_id varchar(50) fk from template
- concept_id varchar(50) not null fk from concept
- question_text text not null
- question_type enum(MCQ / MSQ / NAT)
- difficulty enum(easy/medium/hard) 
- explaination text
- source enum(PYQ / AI / curated)
- created_at timestamp 

QuestionOption
- id int primary key auto_increment
- question_id fk from question
- option_text text not null
- is_correct boolean

Template
- id int primaey key
- concept_id varchar(50) not null fk from concept
- template_type (math/logic/graph)
- difficulty_range 

MockTest
- id int primary key auto-increment
- title varchar(100)
- exam_type ENUM('CSE','DA')
- created_by (FK user/admin/AI)
- total_marks int default 100
- total_questions int default 65
- duration_minutes int default 180
- is_generated BOOLEAN   ← AI or prebuilt
- created_at timestamp default current_timestamp

MockQuestion
- id int primary key
- mock_id  varchar(50) fk from mocktest
- question_id varchar(50) fk from question
- question_order int 
- marks

StudentAttempt
- id int auto-increment primary key
- user_id int fk from user
- mock_id varchar(50) fk from mocktest
- score int gefault 0
- started_at timestamp
- completed_at timestamp
- status ENUM('in_progress','completed','submitted')

AttemptAnswer
- id int primary key auto-increment
- attempt_id int fk from StudentAttempt
- question_id int fk from Question
- selected_option_id int null
- answer_text text null for NAT
- is_correct boolean
- marks_awarded int

AttemptOption
- id (PK)
- attempt_answer_id (FK)
- option_id (FK)

TopicPerformance
- id
- user_id
- concept_id
- accuracy
- attempts
- last_updated

MockAnalytics
- id
- attempt_id
- time_per_question
- accuracy_per_topic (JSON)

add indexes  
Question(concept_id)
MockQuestion(mock_id)
StudentAttempt(user_id)
AttemptAnswer(attempt_id)
