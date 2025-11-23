# ghkrxhd
import random

def get_positive_int(prompt):
    while True:
        try:
            value = int(input(prompt))
            if value <= 0:
                print("양수를 입력해주세요.")
                continue
            return value
        except ValueError:
            print("숫자를 입력해주세요.")

def monty_hall_simulation(num_doors, num_open, trials=100000):
    stay_wins = 0
    switch_wins = 0

    for _ in range(trials):
        prize = random.randint(1, num_doors)
        choice = random.randint(1, num_doors)

        remaining = [d for d in range(1, num_doors+1) if d not in (prize, choice)]
        opened = random.sample(remaining, num_open)

        # 스테이 전략
        if choice == prize:
            stay_wins += 1

        # 스위치 전략
        closed = [d for d in range(1, num_doors+1) if d not in opened and d != choice]
        new_choice = random.choice(closed)

        if new_choice == prize:
            switch_wins += 1

    stay_prob = round(stay_wins / trials, 2)
    switch_prob = round(switch_wins / trials, 2)

    return stay_prob, switch_prob

if __name__ == "__main__":
    while True:
        N = get_positive_int("전체 문의 개수 N을 입력: ")
        if N < 2:
            print(f"전체 문의 개수는 3개 이상이어야 합니다.")
        K = get_positive_int("몬티가 열어줄 문의 개수 K를 입력: ")
        if N < K + 2:
            print(f"전체 문의 수는 몬티가 열어주는 문 수보다 2 이상 커야 합니다. (현재 N={N}, K={K})")
        else:
            break

    stay_prob, switch_prob = monty_hall_simulation(N, K)

    print("\n=== 결과 ===")
    print(f"바꾸지 않을 때 상품 확률: {stay_prob}")
    print(f"바꿀 때 상품 확률: {switch_prob}")
    print(f"바꾸지 않을 때 꽝 확률: {round(1 - stay_prob, 2)}")
    print(f"바꿀 때 꽝 확률: {round(1 - switch_prob, 2)}")
