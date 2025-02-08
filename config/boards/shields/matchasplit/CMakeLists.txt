# Register the matchasplit shield
board_set_shield(NAME matchasplit)

# Define the left and right versions of the shield
if(CONFIG_SHIELD_MATCHASPLIT_LEFT)
    board_set_shield(NAME matchasplit_left PARENT matchasplit)
endif()

if(CONFIG_SHIELD_MATCHASPLIT_RIGHT)
    board_set_shield(NAME matchasplit_right PARENT matchasplit)
endif()
