extends CharacterBody2D

@export var wander_direction : Node2D
var can_move = true

func _physics_process(_delta):
	move_and_slide()
	if can_move:
		velocity = wander_direction.direction * 200
	if velocity.x > 1:
		$Walk_right.show()
		$Walk_right.play("walk_right")
	elif velocity.x < 1:
		$Walk_left.show()
		$Walk_left.play("walk_left")
	if velocity.y < 1:
		$Walk_up.show()
		$Walk_up.play("walk_up")
	elif velocity.y > 1:
		$Walk_down.show()
		$Walk_down.play("walk_down")
	if !can_move:
		velocity = wander_direction.direction * 0

func _on_timer_timeout():
	can_move = true
	$Looking.stop()
	$Looking.hide()
# (\_/)
# (o.o)
# (> /
#('''''''''''')==============D
#(''''''''''''')
#(@@@@@@@@@@@@@@@)

func _on_wander_got_to_point():
	print("I touched something!")
	$Timer.start()
	can_move = false
	$Looking.show()
	$Looking.play("looking")
